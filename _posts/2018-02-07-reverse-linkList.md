---
layout: post
title: Reverse LinkedList
key: 20180207
tags: leetcode python linkedlist
---

I just did a problem in leetcode about Palindrome Linked List:
Given a singly linked list, determine if it is a palindrome.

It is interesting, to deal with this problem, first you should know reverse linkedlist.
Reverse a singly linkedList has two ways.


# Using Stack to reverse
This method says that you push nodes in stack, until you meet with last node and set it head.
Then pop stack to let it be head.next. I would not explore it too much, I'd like to introduce you the next way.

# Better implementation
This way you just need extra O(1) space.
```python
def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        res = None
        while head:
            res,res.next,head = head,res,head.next
        return res
```
Pretty simple. Every iteration, you update res to new head then update new res's next to previous res. I like this way.
 
# For Palindrome Linked List
After you know reverse, you can deal with palindrome by reverse half of list and compare.
```python
class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
     
        slow = fast = head
        rev = None
        while fast and fast.next:
            rev, rev.next, slow = slow, rev, slow.next
            fast = fast.next.next
        if fast:
            slow = slow.next
        while rev:
            if rev.val != slow.val:
                return False
            res = res.next
            slow = slow.next
        return True
```
