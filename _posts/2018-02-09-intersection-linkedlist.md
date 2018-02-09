---
layout: post
title: Intersection of Two Linked Lists
key: 20180209
tags: leetcode python linkedList
---

# Intersection of Two Linked Lists
Example as below:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```
I considered four ways to implement this problem.
1. Brute Force
Complexity Analysis
Time complexity : O(mn)O(mn).
Space complexity : O(1)O(1).
For each node ai in list A, traverse the entire list B and check if any node in list B coincides with ai.


2. Hash Table
Complexity Analysis
Time complexity : O(m+n)O(m+n).
Space complexity : O(m)O(m) or O(n)O(n).
Traverse list A and store the address / reference to each node in a hash set. Then check every node bi in list B: if bi appears in the hash set, then bi is the intersection node.


3. Reverse Two Lists
Complexity Analysis
Time complexity : O(max(n,m)).
Space complexity : O(1).
Reverse A and B, then compare from start, if ai appears different from bi, then ai-1 is the intersection node.
```python 
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if not headA or not headB:
            return None
        A = B = None
        nextA, nextB = headA, headB
        while nextA and nextB:
            A, A.next, nextA = nextA, A, nextA.next
            B, B.next, nextB = nextB, B, nextB.next
        
        while nextA:
            A, A.next, nextA = nextA, A, nextA.next
        while nextB:
            B, B.next, nextB = nextB, B, nextB.next
        if A != B:
            return None
        intersection = A
        while A == B and A and B:
            A = A.next
            B = B.next
            intersection = A
        return intersection
```
4. Two Pointers
Complexity Analysis
Time complexity : O(m+n).
Space complexity : O(1).
This is a little more tricky, that say we have two pointers pAand pB pointing to A and B. Then we iterate pA and pB, if pA meets end of A and let it point to B, so does pB. So eventually if they have intersection it will appear in second iteration, because assume A.length - B.length = n, first iteration
pB meets end of B but pA still have n nodes. Then pB points to A, when A meets end, pB have B.length nodes. So when pA points to B, this iteration they just have same node to iterate.
```python
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if not headA or not headB:
            return None
        pA,pB = headA,headB
        while pA != pB:
            pA = headB if not pA else pA.next
            pB = headA if not pB else pB.next
        return pA
```