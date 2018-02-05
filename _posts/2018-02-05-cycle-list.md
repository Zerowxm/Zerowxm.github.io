---
layout: post
title: Linked List Cycle
key: 20180205
tags: leetcode python linkedList
---

# Linked List Cycle
Given a linked list, determine if it has a cycle in it.

# Implementation
There are two ways, first is to use extra space to store visited node.
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        visitedNode = set()
        if not head:
            return False
        while head:
            if head not in visitedNode:
                visitedNode.add(head)
            else:
                return True
            head = head.next
        return False
```

Another way is using two pointers, one moves one step, the other moves two steps.
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
		fast, slow = head, head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True
        
        return False
```