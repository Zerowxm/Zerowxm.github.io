---
layout: post
title: Top K Frequent Elements
key: 20180204
tags: leetcode python array
---

# Merge Sorted Array
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

# Implementation
The idea is to merge them from end to start.
```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        
        m,n,k = m - 1,n - 1,m + n - 1
        while m >= 0 and n >= 0:
            if nums1[m] > nums2[n]:
                nums1[k] = nums1[m]
                k -= 1
                m -= 1
            else:
                nums1[k] = nums2[n]
                k -= 1
                n -= 1
        nums1[:n+1] = nums2[:n+1]
```

Another method is to use build-in sort.
```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        nums1[m:] = nums2[:]
        nums1.sort()
```