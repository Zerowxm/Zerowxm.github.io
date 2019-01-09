---
layout: post
title: Dictionary sort
key: 20180322
tags: python
---

Given an encoding rule, a(1),b(2),c(3)...z(26),ab(27),ac(28)...
alphabet is ascending order and never duplicate.
Givn a string, calculate the encoded number.

Here we define f(i, k) to be # of string beginning with ith alphabet and k length,
define g(k) to be sum of # of all strings with length k.

```python
class AlphabetEncode:
  def f(i, k):
		if k == 1:
		  return 1
		sum = 0
		for j in range(i+1, 27):
		  sum += f(j, k-1)
		return sum

	def g(k):
	  sum = 0
	  for i in range(1,27):
        sum += f(i, k)

    def alpha2ascii(n):
      ord(n) - ord('a') + 1

    def encode(self, s):
  	  sum = 0
  	  k = len(s)
  	  for i in range(1, k):
  	    sum += g(k)

  	  start = alpha2ascii(s[0])

  	  for j in range(1, start):
  	    sum += f(j, k)

  	  for i in range(1,k):
  	    h = alpha2ascii(s[i])

  	    len = k - i
  	    for j in range(start, h):
  	      sum += f(j, len)
  	      start = h
  	  return sum + 1

```
