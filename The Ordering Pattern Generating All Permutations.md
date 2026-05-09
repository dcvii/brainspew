---
title: "The Ordering Pattern: Generating All Permutations"
source: https://newsletter.francofernando.com/p/the-ordering-pattern-generating-all?publication_id=1172544&post_id=82350676&isFreemail=true&r=7br8e&triedRedirect=true
author:
  - "[[Franco Fernando]]"
published: 2026-05-09
created: 2026-05-09
description: How to find every possible arrangement of a set of items
tags:
  - brain_spew
  - askew
---
Hi Friends,

Welcome to the 172nd issue of the Polymathic Engineer newsletter.

In the last article in our series on recursion, we looked at the selection pattern, which lets us find all possible subsets of a set. The most important question was whether or not to include each item.

In this article, we shift our focus from which items to include to how to arrange them. This is the ordering pattern, and its purpose is to generate all permutations of a set of items.

The difference between combinations and permutations is easy. With combinations, \[1, 2\] and \[2, 1\] are the same because the order of the elements does not matter. With permutations, the order matters. A set of three items, such as \[1, 2, 3\], has 8 possible subsets but 6 possible permutations: \[1, 2, 3\], \[1, 3, 2\], \[2, 1, 3\], \[2, 3, 1\], \[3, 1, 2\], \[3, 2, 1\].

Ordering problems come up a lot in practice. Every time you need to find all possible ways to arrange, schedule, or sequence anything, you need to generate permutations. And, like selection, the ordering pattern employs backtracking to consider all options.

The outline is as follows:

- The Core Ordering Pattern
- The Swap-Based Approach
- Permutations of Specific Length
- Handling Duplicates in the Input
- Application: Binary Search Tree Orderings
- When Ordering Applies

---

Project-based learning is the best way to develop technical skills. [CodeCrafters](https://app.codecrafters.io/join?via=FrancoFernando) is an excellent platform for tackling exciting projects, such as building your own Redis, Kafka, a [DNS server](https://app.codecrafters.io/join/dns-server?via=francofernando), SQLite, HTTP server or Git from scratch using your favourite programming language. Noe you can also try to build your own Claude Code (for free, still in beta).

[Sign up, and become a better software engineer](https://app.codecrafters.io/join?via=FrancoFernando).

---

## The Core Ordering Pattern

While selection goes through each item and asks whether to include it, ordering takes a different approach. Instead of making include/exclude decisions, it asks: which item comes next?

The underlying idea is to keep a set of available items. At each step, we pick one item from the set, add it to our current permutation, remove it from the set, and recursively find all permutations of the remaining items. When there are no remaining items, we have built one complete permutation.

Let’s start with a simple example, with three items: \[1, 2, 3\]. In the beginning, all items are available. We could choose 1 first, which leaves us with \[2, 3\]. From there, we could pick 2, which leaves us with only \[3\]. Then we can only choose 3, and now we have our first permutation: \[1, 2, 3\].

At this point, we backtrack. We put 3 back, put 2 back, and try picking 3 instead. This gives us \[1, 3, 2\]. We continue this process, trying every possible first item, then every possible second item, and so on.

The following code snippet shows how to implement this:

```markup
def permutations(items):
    result = []
    available = set(items)
    
    def helper(path):
        if not available:
            result.append(path[:])
            return
        
        for item in list(available):
            available.remove(item)
            path.append(item)
            helper(path)
            path.pop()
            available.add(item)
    
    helper([])
    return result
```

The structure is quite similar to what we have seen with selection. We have a helper function that builds the permutation step by step. The base case is when there are no items left to choose from, meaning we have used all of them and produced a complete permutation.

In the recursive step, we go through each available item. We take each one out of the set, add it to the path, and call the function again. After the call is over, we go back by taking the item off the path and putting it back in the set.

One thing to note is that we iterate over a copy of the list of available items instead of iterating over them directly. This is because we are modifying the set inside the loop, and most languages do not allow you to change a collection while iterating over it.

![](https://substackcdn.com/image/fetch/$s_!J-kl!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F32f854f5-339c-40ea-8ab6-97762544414f_1912x863.png)

The time complexity is O(n! × n). The branching factor starts at n and decreases by one at each level, which gives us n × (n-1) × (n-2) ×... × 1 = n! paths. Each time we complete a permutation, we then need O(n) time to copy it into the result. The space complexity is O(n) for the recursion stack and the path we are building.

## The Swap-Based Approach

The set-based approach we looked at is straightforward, but there is a more efficient way that you can also use in interviews. This method does not store a separate list of available items. Instead, it uses the input array itself to track what has been used and what remains available.

The underlying idea is to divide the array into two parts using an index. All the items before the index already belong to the permutation we are generating. The items from the index onward are the pool of items we can still choose from. At each step, we swap an item from the available portion into the current position and then move to the next index. Let’s go back to our simple example, \[1, 2, 3\], to grasp how the process works.

Initially, the index is equal to 0 because the entire array is available. We swap the first item with itself, which doesn’t change anything, then we move to index 1. We can now choose either 2 or 3. We choose 2 and swap the second item with itself. Then we go to index 2, pick 3, and get our first permutation: \[1, 2, 3\]. At this point, we backtrack.

We go back to index 1 and swap positions 1 and 2. This places 3 in position 1 and 2 in position 2, yielding \[1, 3, 2\]. We keep doing this until we have executed every potential swap at every slot.

The following code snippet shows how to implement this:

```markup
def permutations(items):
    result = []
    
    def helper(index):
        if index == len(items):
            result.append(items[:])
            return
        
        for j in range(index, len(items)):
            items[index], items[j] = items[j], items[index]
            helper(index + 1)
            items[index], items[j] = items[j], items[index]
    
    helper(0)
    return result
```

The structure is very similar to the set-based version. The base case is when our index reaches the end of the array. This means that we have made a choice for every position and produced a complete permutation.

In the recursive step, we go through each item from the current index to the end. For each item, we swap it into the current position, call the function again with the next index, and then swap it back to restore the original order.

The best thing about this method is that we don't have to make copies of the available items at every step. We are directly changing the order of the elements in the array. In practice, this makes it a bit more efficient, even though the worst-case analysis stays the same: O(n! × n) for time and O(n) for space.

## Permutations of Specific Length

Sometimes we don’t need all the possible permutations of a set, but only those of a specific length. For example, if we have \[1, 2, 3, 4\], we could want all the two-length permutations: \[1, 2\], \[1, 3\], \[1, 4\], \[2, 1\], \[2, 3\], and so on.

Hi **mbowen@mdcbowen.org**

## This post is for paid subscribers

[Already a paid subscriber? **Switch accounts**](https://substack.com/sign-in?redirect=%2Fp%2Fthe-ordering-pattern-generating-all%3Fpublication_id%3D1172544%26post_id%3D82350676%26isFreemail%3Dtrue%26r%3D7br8e%26triedRedirect%3Dtrue&for_pub=francofernando&change_user=true)