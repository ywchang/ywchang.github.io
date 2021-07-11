---
layout: post
title:  "Max Sum of Rectangle No Larger Than K"
date:   2021-07-10 20:27:00 +0800
categories: algorithm
---

This post is trying to solve a problem showing up recently in monthly challenge. It's been marked as a hard problem, and it's probably easy to be clueness when first met because it needs to combine several tricks together to solve it effectively.

Below is the problem of `Max Sum of Rectangle No Larger Than K`. 

Given an `m x n` matrix `matrix` and an integer `k`, return the max sum of a rectangle in the matrix such that its sum is no larger than `k`.

It is guaranteed that there will be a rectangle with a sum no larger than `k`.

Example 1:

![Grid Sum](https://github.com/ywchang/ywchang.github.io/blob/master/_imgs/2021-07-10-example-grid-sum.jpeg?raw=true)

```
Input: matrix = [[1,0,1],[0,-2,3]], k = 2
Output: 2
Explanation: Because the sum of the blue rectangle [[0, 1], [-2, 3]] is 2, and 2 is the max number no larger than k (k = 2).
```

Example 2:

```
Input: matrix = [[2,2,-1]], k = 3
Output: 3
```

And this is the original link for above problem, [https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)

So, to get the max sum of a rectangle in the matrix such that its sum is no larger than k, a very natural idea is to iterate all the rectangles, get sum of each rectangle, and choose the largest one among the sums that are no larger than k. But maybe it doesn't take too long to realise that there are just too many rectangles to iterate. For example, let's look at the Example 1 above. For the 2x3 matrix, there are in total 18 rectangles already!

Let's probably pause here for a little bit. Instead of trying to come up with solution for a matrix, let's take a step back and think about what solution we can come up with if this is an array, which has only one dimension. Actually there are some links related to this problem on stackoverflow, like this one [https://stackoverflow.com/questions/39084147/largest-sum-of-contiguous-subarray-no-larger-than-k](https://stackoverflow.com/questions/39084147/largest-sum-of-contiguous-subarray-no-larger-than-k). But anyway, the problem statement is something like below. 




<script src="https://utteranc.es/client.js"
        repo="ywchang/ywchang.github.io"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>










