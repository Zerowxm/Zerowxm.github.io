---
layout: post
title: Top K Frequent Elements
key: 20180128
tags: leetcode python hashtable
---

# [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)
Given a non-empty array of integers, return the k most frequent elements.

For example,
Given `[1,1,1,2,2,3]` and `k = 2`, return `[1,2]`.

Note: 
* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

In this problem, the key is to count frequency of elements in the given list, then find k elements who has the most frequency, there are three ways to solve it in python.

# 1. Use list index to refer the frequency.
First, we could use collections.Counter to count frequency of list elements.
	`c = collections.Counter(nums)`
Then, we create a zero-list with  nums-length + 1 elements.
	`mapF = [0] * (len(nums) + 1)`
Third, to iterate `c`, frequency <= nums-length, so use frequncy as index to store the element in another list.
```python
	for n in  c:
	    if mapF[c[n]] == 0:
	        mapF[c[n]] = [n]
	    else:
	        mapF[c[n]].append(n)
```
Finally, iterate `mapF` from end to start, return the first k elements.
```python
	i = len(mapF) - 1
    while i != 0 and len(ans) < k:
        if mapF[i] != 0:
            ans.extend(mapF[i])
        i -= 1
    return ans
```

# 2. Use Counter.most_common
```ptyon
c = collections.Counter(nums)
return [x[0] for x in c.most_common(k)]
```

# 3. Use Sort
```ptyon
return [x for x, count in sorted(Counter(nums).items(), key = lambda y: y[1], reverse = True)[ : k]]
```