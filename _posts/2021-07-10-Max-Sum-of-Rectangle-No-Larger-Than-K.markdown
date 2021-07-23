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

Let's say we have a array, `[2, 2, -1]`, then we need to know the max subarray sum which can't be larger than `k`.

If `k = 0`, then the resut is -1, which the subarray is `[-1]`
If `k = 3`, then the result is 3, which the subarray is `[2, -1]`

How do you solve this problem? Here, we keep hearing the subarray sum, so probably a handy tool that we can use to make calculating subarray sum easier, which is `prefix sum` or `cumulative sum` data structure.

So the `prefix sum` data structure can help to make the calculation of subarray sum very fast with O(1) time complexity. Let's imagine we have a array `[1, 2, 3, 4]`, and then the corresponding prefix sum will be `[1, 3, 6, 10]`. Thus in order to calculate the subarray sum with index range `[1, 2]`, we just need to use `prefix_sum[2] - prefix_sum[0]`, instead of selecint the proper elements and sum them up everytime. You probably have found out that we can't calcualte the subarray sum with range starting at 0, because then we will have prefix_sum[-1] which is not legal. That's totally right, and that's why in practice we pad a 0 in the very beginning to work around that, in that sense, the example above will have a prefix sum like `[0, 1, 3, 6, 9]`. Then generally a calculation of range [i, j] can be converted to `prefix_sum[j + 1] - prefix_sum[i]`. 

Below are some legit Java codes to demonstrate how to use prfix sum data structure to calculate any subarray sum by giving a range index (both inclusive).

```
public class TryPrefixSum {
        public int calculateSubArraySum(int[] arr, int start, int end) {
                int[] prefixSum = getPrefixSum(arr);
                return prefixSum[end + 1] - prefixSum[start];
        }

        private int[] getPrefixSum(int[] arr) {
                int[] prefixSum = new int[arr.length + 1];
                prefixSum[0] = 0;
                for(int i = 0; i < arr.length; i++) {
                        prefixSum[i + 1] = arr[i] + prefixSum[i];
                }
                return prefixSum;
        }       

        public static void main(String[] args) {
                System.out.println(
                        new TryPrefixSum().calculateSubArraySum(new int[] {1, 2, 3, 4}, 0, 2)
                ); // => 6
                System.out.println(
                        new TryPrefixSum().calculateSubArraySum(new int[] {1, 2, 3, 4}, 1, 2)
                ); // => 5
        }
}
```

With above knowledge, now we can try to solve the `no larger than K` part. Let's refresh by repeating the problem statement again.

Let's say we have a array, `[2, 2, -1]`, then we need to know the max subarray sum which can't be larger than `k`.

If `k = 0`, then the resut is -1, which the subarray is `[-1]`
If `k = 3`, then the result is 3, which the subarray is `[2, -1]`

Suppose with index i, we have Sum[i+1] to be the related prefix sum. Then we can iterate from Sum[0] to Sum[i], let's mark it as Sum[j]. For each Sum[j], we use d = Sum[i] - Sum[j]. Then we can find the best d for index i, which is no larger than k, but it's the clostest. Cleary we can have a optimization here, if we find the d is equal to k, then we can just stop finding, and return k directly. So if the array size is N, we will have time complexity being O(N\*N). Can we do better at finding the d more efficiently for each index i?


<script src="https://utteranc.es/client.js"
        repo="ywchang/ywchang.github.io"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>










