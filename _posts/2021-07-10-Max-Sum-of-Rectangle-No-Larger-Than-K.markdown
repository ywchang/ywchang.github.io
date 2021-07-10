---
layout: post
title:  "Max Sum of Rectangle No Larger Than K"
date:   2021-07-10 20:27:00 +0800
categories: algorithm
---

This post is trying to solve a problem showing up recently in monthly challenge. It's been marked as a hard problem, and it's probably easy to be clueness when first met because it needs to combine several tricks together to solve it effectively.

#### The problem - Max Sum of Rectangle No Larger Than K

Given an `m x n` matrix `matrix` and an integer `k`, return the max sum of a rectangle in the matrix such that its sum is no larger than `k`.

It is guaranteed that there will be a rectangle with a sum no larger than `k`.

Example 1:

![Grid Sum](../_imgs/2021-07-10-example-grid-sum.jpeg)

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


<script src="https://utteranc.es/client.js"
        repo="ywchang/ywchang.github.io"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>










