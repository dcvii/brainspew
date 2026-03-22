---
title: "Recursion in Practice: Iteration and Subproblems"
source: "https://newsletter.francofernando.com/p/recursion-in-practice-iteration-and?publication_id=1172544&post_id=189814178&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Franco Fernando]]"
published: 2026-03-21
created: 2026-03-22
description: "How to apply the first two recursive patterns to real problems."
tags:
  - "brain_spew"
---
### How to apply the first two recursive patterns to real problems.

Hi Friends,

Welcome to the 165th issue of the Polymathic Engineer. This week, we keep going our recursion series with the second article.

In the [previous article](https://newsletter.francofernando.com/p/mastering-recursion-the-foundations), we covered the foundations: base cases, recursive steps, return strategies, tracing code, and complexity analysis. Now it’s time to put those basics to work.

This article covers the first two recursive patterns: Iteration and Subproblems. These are the most approachable patterns and a natural starting point before tackling all the others.

The outline is as follows:

- The Iteration pattern
- Iterating forward and backward over arrays
- Inserting at the bottom of a stack
- Nested iteration with recursion
- The Subproblems pattern
- Towers of Hanoi
- Checking if a string is a palindrome
- The stair step problem

---

Project-based learning is the best way to develop technical skills. [CodeCrafters](https://app.codecrafters.io/join?via=FrancoFernando) is an excellent platform for tackling exciting projects, such as building your own Redis, Kafka, a [DNS server](https://app.codecrafters.io/join/dns-server?via=francofernando), SQLite, or Git from scratch. [Sign up, and become a better software engineer](https://app.codecrafters.io/join?via=FrancoFernando).

---

## The Iteration Pattern

The iteration pattern is the simplest of the six. The basic idea is to replace a for loop with a recursive function. Each recursive call handles a step of the iteration, and the base case is when there are no more elements to process.

At first, this may seem like a waste of time. Why change a for loop that already works to recursion? There are a few times when it makes sense.

The first is when you need to access data in reverse order. Consider printing a linked list backward. With iteration, you would have to push all the values onto a stack and then pop them off. With recursion, the call stack does this for you automatically. The code becomes shorter and easier to follow.

The second is when the recursion takes care of memory for you. Some problems need temporary storage that matches the structure of the input. You don’t have to explicitly create and manage that storage yourself; instead, you can let the recursive calls hold the data in their stack frames. We will see a concrete example of this when we insert an element at the bottom of a stack.

The third is when you use functional programming. Languages like Haskell or certain styles of JavaScript avoid mutable state entirely. Recursion takes the place of loops in these contexts because there is no loop that doesn’t change a counter variable.

There is one thing to keep in mind: the iteration pattern doesn’t usually improve time complexity. Most of the time, the recursive version does the same amount of work as the iterative one. The advantage is that the code is cleaner, not that it runs faster. And since recursion uses stack frames, it can actually use more memory than a simple loop.

When you use this pattern, there are two questions to ask yourself. The first is: what is the iterative step? In a regular for loop, this might be i + 1, or i + 2, or something more complex. Your recursive call will mirror this. The second is: which way do you want to go? Going forward or backward? The answer affects where you put the recursive call relative to the work you do in each step. We'll see both directions in the next section.

## Iterating Forward and Backward

Let’s start with a simple example: print every element in an array. Here is the iterative version (I know the code is not pythonic but it is better for the sake of the examples):

```markup
def print_array(arr):

    for i in range(len(arr)):

        print(arr[i])
```

To make this code recursive, we need to think about what happens at each step of the iteration. In this case, we move from index i to index i + 1. The base case occurs when the index reaches the array's length, which means that there are no more elements to print. The recursive version does the same. It prints the current element, then moves to the next. When it runs out of elements, it stops.

```markup
def print_array(arr, i=0):
    if i == len(arr):
        return

    print(arr[i])
    print_array(arr, i + 1)
```

Now here is something interesting. If you swap the order of the last two lines, you get the array printed in reverse:

```markup
def print_array_reverse(arr, i=0):
    if i == len(arr):
        return

    print_array_reverse(arr, i + 1)
    print(arr[i])
```

The only change is that the print statement comes after the recursive call. This means we first go to the end of the array, then print the elements as the calls come back. The last element in the array is printed first, and so on.

This is a pattern you will see often: the order of the recursive call relative to the work determines the direction of processing. If you do the work first and then recurse, you process forward. If you recurse first and then do the work, you process backward.

You can use the same idea when you want to return a result rather than print it. As we discussed in the first article, you can either use a passed variable or build up the result as you return. Here is an example that sums all the elements in an array with the build-up approach:

```markup
def sum_array(arr, i=0):
    if i == len(arr):
        return 0

    return arr[i] + sum_array(arr, i + 1)
```

The function finds the sum from index i to the end. The base case says that the sum of an empty slice is 0. The recursive step states that the sum is the current element plus the sum of everything after it. As the calls return, the values add up.

If you prefer using a passed variable, the code looks like this:

```markup
def sum_array(arr, i=0, result=None):
    if result is None:
        result = [0]

    if i == len(arr):
        return result[0]

    result[0] += arr[i]
    return sum_array(arr, i + 1, result)
```

Both approaches lead to the same answer. The build-up version is usually cleaner for simple cases, while the passed-variable can be better as the logic gets more complex.

## Inserting at the Bottom of a Stack

Now, let’s look at a problem where recursion does more than just take the place of a for loop. You have to put something at the bottom of a stack without using any extra data structures.

![](https://substackcdn.com/image/fetch/$s_!HcFg!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9e94954f-53d6-42d3-ace9-615351e76822_448x443.png)

If you try to do this iteratively, you run into a problem. You can only access the top of a stack, so you have to pop everything off, insert your item, and push everything back on. This requires a temporary stack to hold the elements (In Python, we use a list as a stack, with append() to push and pop() to remove from the top):

```markup
def insert_at_bottom_iterative(stack, item):
    temp = []
    while stack:
        temp.append(stack.pop())

    stack.append(item)
    while temp:
        stack.append(temp.pop())
```

The code works, but you need to create and maintain the temporary stack. When you use recursion, the call stack takes care of this implicitly. The recursive approach pops elements off one at a time, makes a recursive call, and then pushes each element back on after the call comes back. The base case is when the stack is empty, at which point we insert the item. As the recursive calls return, each previously popped element gets pushed back on top:

```markup
def insert_at_bottom(stack, item):
    if not stack:
        stack.append(item)
        return

    top = stack.pop()
    insert_at_bottom(stack, item)
    stack.append(top)
```

Let’s trace through this with a concrete example. Suppose the stack is \[1, 2, 3, 4\] (with 4 on top) and we want to insert 5 at the bottom.

The first call pops 4 and saves it. The stack is now \[1, 2, 3\]. The second call pops 3. The stack is \[1, 2\]. The third call pops 2. The stack is \[1\]. The fourth call pops 1, leaving the stack empty.

Now we hit the base case. We append 5, so the stack is \[5\]. Then the calls start coming back. The fourth call appends 1, giving us \[5, 1\]. The third call appends 2, giving us \[5, 1, 2\]. The second call appends 3, giving us \[5, 1, 2, 3\]. The first call appends 4, and we end up with \[5, 1, 2, 3, 4\].

The time complexity is O(n) because we need to pop and push each element once. The space complexity is also O(n) since the call stack must hold all popped elements. This is the same as the iterative version, but the recursive code is shorter and easier to read.

## Nested Iteration with Recursion

Hi **mbowen@mdcbowen.org**

## This post is for paid subscribers

[Already a paid subscriber? **Switch accounts**](https://substack.com/sign-in?redirect=%2Fp%2Frecursion-in-practice-iteration-and%3Fpublication_id%3D1172544%26post_id%3D189814178%26isFreemail%3Dtrue%26r%3D7br8e%26triedRedirect%3Dtrue&for_pub=francofernando&change_user=true)