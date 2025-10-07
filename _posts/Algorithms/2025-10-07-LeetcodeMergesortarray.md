---
title: "Leetcode #88 : Merge Sorted Array"
date: 2025-10-07
toc: true
toc_sticky: true
use_math: true
categories:
  - algorithms
---

[Link](https://leetcode.com/problems/merge-sorted-array/?envType=study-plan-v2&envId=top-interview-150)

# Question
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m` + `n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to 0 and should be ignored. `nums2` has a length of `n`.

# Prerequisites
1. Two pointer techniques : To manipulate two arrays simultaneously, we use the two pointer method. After each element is used, the pointer to the corresponding array is decreased by one.

2. In place array manipulation : Final results should be stored inside the array `nums1`

3. Working Backward

4. Non-decreasing order

5. Edge cases : We need to consider whether a single array is lacking elements.

6. Time complexity : We required to design linear time complexity. 

# Solution
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        p1 = m-1
        p2 = n-1
        p = m+n-1

        while p1>=0 and p2>=0:
            if nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -=1
            p -= 1
        while p2 >= 0:
            nums1[p] = nums2[p2]
            p2 -=1
            p -=1
```

# Example

Let's consider the case **nums1 = [1,2,3,0,0,0], nums2 = [2,5,6]**

| Iteration / Comparison | `nums1[p1]` vs `nums2[p2]` | Action | `p1`  | `p2`  | `p`  | State of `nums1` |
| :---: | :---: | :--- | :---: | :---: | :---: | :--- |
| **Initial State** | - | Set pointers | `2` | `2` | `5` | `[1, 2, 3, 0, 0, 0]` |
| **Iteration 1** | `3` vs `6` | `nums1[5] = 6` (Copy from `nums2`) | `2` | `1` | `4` | `[1, 2, 3, 0, 0, 6]` |
| **Iteration 2** | `3` vs `5` | `nums1[4] = 5` (Copy from `nums2`) | `2` | `0` | `3` | `[1, 2, 3, 0, 5, 6]` |
| **Iteration 3** | `3` vs `2` | `nums1[3] = 3` (Copy from `nums1`) | `1` | `0` | `2` | `[1, 2, 3, 3, 5, 6]` |
| **Iteration 4** | `2` vs `2` | `nums1[2] = 2` (Copy from `nums2`) | `1` | `-1`| `1` | `[1, 2, 2, 3, 5, 6]` |
| **End** | - | Loop ends (`p2 < 0`) | `1` | `-1`| `1` | `[1, 2, 2, 3, 5, 6]` |