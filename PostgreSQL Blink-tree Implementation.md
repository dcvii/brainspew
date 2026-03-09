---
title: "PostgreSQL Blink-tree Implementation"
source: "https://www.alibabacloud.com/blog/postgresql-blink-tree-implementation_602913"
author:
published:
created: 2026-03-08
description:
tags:
  - "brain_spew"
---
---

*By Baotiao*

## Lehman blink-tree and Vladimir Lanin concurrent Btree

The PostgreSQL blink-tree implementation references two articles:

- *Lehman and Yao's high-concurrency B-tree management algorithm*
- *V. Lanin and D. Shasha, A Symmetric Concurrent B-Tree Algorithm*

The B-tree implementation of MySQL InnoDB mainly refers to *R. Bayer & M. Schkolnick Concurrency of operations on B-trees March 1977*

## Lehman blink-tree

Two core changes of the Blink-tree

1\. Adding a single "link" pointer field to each node.

Here is the background at that point in time. In most B-tree implementations we see now, there are left and right pointers pointing to the left and right pages. However, the definition of the standard B-tree at that time did not have this requirement. In a B-tree, non-leaf nodes also store data. In a B+tree, only leaf nodes store data, which keeps the B-tree height as low as possible. However, there is no strict requirement to connect leaf nodes together.

However, generally speaking, for a B-tree, there is no mandatory requirement to have left and right pointers pointing to the left and right pages.

Such as the B-tree in InnoDB, it already includes leaf page and right page pointers. At the same time, at different levels, the left and right pointers of leaf and non-leaf nodes point to their sibling nodes.

Therefore, the right page pointer can now be reused with the link page pointer.

2\. Add a high key field in each node. During a query, if the target value exceeds the high key of the node, you need to follow the link pointer to continue searching in the successor node.

![1](https://yqintl.alicdn.com/3c642b35766b7e74a7f7a3da9a39d0b2ec84ed27.jpeg "1")

Therefore, the major difference from the blink-tree of PolarDB is that the lock-coupling operation is canceled, and the search operation does not apply locks.

## PolarDB blink-tree

The search operation is performed through the lock-coupling operation, which performs locking and unlocking operations from top to bottom.

The Structure Modification Operation (SMO) does not involve lock-coupling. It first locks the child node, then releases the child node, and then locks the parent node. The details are:

When the leaf page is locked and the operation is completed to insert into the parent node, you need to release the page lock of the child node, then search the B-tree again to find the parent node, add a page lock, and modify it. Of course, you can also save the parent node pointer to avoid the second search operation, but this is an optimization.

In the standard blink-tree, which is the PostgreSQL Blink-tree

The search operation does not involve lock coupling. Instead, it only needs to add the latch of the current layer. Between finding the child page ID and obtaining the child page, because there is no lock-coupling, no latch is held during the period from releasing the parent node latch to adding the child node latch. Therefore, if an SMO occurs in the child page and the record to be searched is no longer in the child page, how should this be handled?

In the PolarDB blink-tree, the lock-coupling operation ensures that the search operation holds both the parent node and child node latches at the same time, so such a situation does not occur.

The following example illustrates such a situation:

The search 15 operation and the insert 9 operation that triggers the SMO are proceeding concurrently.

15 was originally in y. When the find(15) operation was performed, y split into y and y'. 15 moved to the new y'.

![2](https://yqintl.alicdn.com/ab234c553b55215ae39ce32188541597ca51704e.jpeg "2")

```
# This is not how it works in postgres. This demonstrates the problem:
"Thread A, searching for 15"   |   "Thread B, inserting 9"
                               |   node2 = read(x);
node = read(x);                |
"Examine node, 15 lies in y"   |   "Examine node2, 9 belongs in y"
                               |   node2 = y;
                               |   # 9 does not fit in y
                               |   # Split y into (8,9,10) and (12,15)
                               |   y = (8,9,10); y_prime = (12,15)
                               |   x.add_pointer(y_prime)
                               |   
"y now points to (8,9,10)!"    |
node = read(y)                 |
find(15) "15 not found in y!"  |
```

For this example, you can see that the PolarDB blink-tree solves the problem through lock-coupling. After the read(x) operation, the node(y)'s lock is held at the same time. Then, when Thread B performs the SMO, it needs to hold the node(y) x lock. Therefore, the SMO is blocked, thereby avoiding the occurrence of the above problem.

**How does the blink-tree introduced by Lehman solve this?**

After the link-page and high key are added in node(y).

The aforementioned find(15) operation determines that 15 > node(y)'s high-key, so the operation searches in node(y)'s link-page. That is y'. Then, you can find 15 on y'.

**Then, how is the Structure Modification Operation (SMO) performed?**

The Lehman Blink Tree SMO operation holds the child node while locking the parent node, and it is a bottom-up latch coupling operation. Because the search operation does not require lock coupling, the bottom-up operation does not cause issues. Therefore, you can hold the child latch while requesting the parent node latch.

Here, the latches of both the child and parent nodes are held simultaneously.

If the parent node also contains a link page at this time, which means insertion into the parent node -> link page is required, then the latches of these 3 pages (child, parent, and parent->link page) must be held simultaneously.

If an insertion point is still not found in the parent->link page and it is necessary to go to the parent->link page->link page, you can release the parent node and then acquire the link page -> link page.

Therefore, latches of at most 3 nodes are held at the same time.

In most cases, there is only one link page, so many operations can be simplified.

Here, there is further optimization in the Vladimir Lanin Concurrent Btree.

According to the current PostgreSQL implementation, if you lock the child node and then insert into the parent node, only one link page appears. Because the page lock is not released before the split ends when the first page splits, a new insertion cannot proceed.

Only when using an approach such as the PolarDB Blink Tree, where the child node latch is released after the insertion into the child node is completed and then the parent node is inserted into, allowing the link page to continue being inserted into during the insertion into the parent node, can the situation of multiple link pages occur.

My understanding is that PostgreSQL also made a trade-off here to avoid the complex situation of multiple link pages.

Although multiple Link-pages do not appear here, it is possible that multiple link pages need to be traversed to reach the target page during a search or insert operation, such as in the following example.

![3](https://yqintl.alicdn.com/cc6529014cf155f0a70f0cac45f78e608d2fd0f0.jpeg "3")

Actually, a method similar to the PolarDB Blink Tree can also be used here. That is, after the child node is inserted, you can release the lock on the child node and re-traverse the B-tree to insert into the parent node, thereby allowing the child node latch to be released as early as possible.

Actually, the Blink Tree article also discussed the remembered list.

We then proceed back up the tree (using our “remembered” list of nodes through which we searched)

Vladimir Lanin **Concurrent Btree**

At the beginning, the implementation methods of B-tree concurrency before the Blink Tree were summarized.

When a search is performed, locking is done top-down with lock coupling. When an SMO is performed, the subtree is locked and locking is done top-down. Because both Search and SMO operations are top-down, deadlocks can be avoided.

What were the drawbacks of the concurrency control methods before this article was published?

1. It is difficult to clearly calculate the range of the lock subtree. This is also a very complicated part of the existing MySQL Code.
2. The scope of concurrency with lock coupling is still insufficient. Here, it is emphasized that lock-coupling does not necessarily need to be used with a Blink Tree. It can also be used with a standard B-tree. In this article, it is used with a B+tree.

Both of these two methods sacrifice concurrency to obtain safety.

Of course, there are also optimization methods for lock coupling + lock subtree, which involve using optimistic locking first and then pessimistic locking. When the optimistic path is taken, S locks are used throughout the path. Then, when the leaf node is found, an X lock is applied only to the leaf node. In this way, in (k-1)/k cases (where 2k represents the number of records in a page), the optimistic path can be taken. In fact, InnoDB uses the method of being optimistic first and then pessimistic.

Other approaches are similar to the Lehman blink-tree, except that during a Structure Modification Operation (SMO), "only lock one node at a time" is achieved. However, this was not implemented in the specific implementation of PostgreSQL. I understand that this is mainly to consider safety.

![4](https://yqintl.alicdn.com/b7deee42c3b196bd60f16e0f1b0551f37d1172b1.jpeg "4")

The article also mentions:

> Although it is not apparent in \[Lehman, Yao 811 itself, the B-link structure allows inserts and searches to lock only one node at a time.

This means that "insert and search only one node" can be achieved, which is also my idea.

> Each action holds no more than one read lock at a time during its descent, an insertion holds no more than one write lock at a time during its ascent, and a deletion needs no more than two write locks at a time during its ascent.

After the completion of a half-split or a half-merge, all locks are released.

It is indeed like this in the article. After a half-split, all locks are released. Then, when the parent node is inserted, the process is similar to the existing approach of PolarDB. That is, all locks are released to re-insert the data of a new layer. This ensures that the SMO operation only locks one layer at the same time.

> Normally, finding the node with the right coverlet for the add-link or remove-link is done as in \[Lehman, Yao 811, by re-accessing the last node visited during the locate phase on the level above the current node. Sometimes (e.g. when the locate phase had started at or below the current level) this is not possible, and the node must-be found by a new descent from the top.

When the parent node is inserted, the insertion can be performed by using the saved memory-list or by traversing again.

In addition, the delete operation, which was not implemented in Lehman's article, is supplemented by using an idea similar to link-page.

![5](https://yqintl.alicdn.com/b7993d5681c3545020f8063d71e29ce8e029591d.jpeg "5")

If compared only with MySQL's InnoDB, the Blink-tree implementation of PostgreSQL is obviously more detailed in lock granularity. While avoiding the Index lock of the entire B-tree, it also avoids the conflict problem between the Search operation and the SMO operation caused by the lock subtree method.

This article introduces PostgreSQL's blink-tree implementation for high-concurrency B-tree operations using link pointers and optimized locking mechanisms.