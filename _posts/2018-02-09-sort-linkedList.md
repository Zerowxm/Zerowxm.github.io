---
layout: post
title: Sort LinkedList
key: 20180209
tags: leetcode python linkedList
---
Sort a linked list in O(n log n) time using constant space complexity.

```python
class Solution(object):
	def sortList1(self, head):
		l = []
            ref = head
            while ref!=None:
                l.append(ref.val)
                ref = ref.next
            l.sort()        
            ref = head
            for i in l:
                ref.val = i
                ref = ref.next
            return head
            
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        valList = []
        nodeTable = {}
        while head:
            val = head.val
            valList.append(val)
            if val in nodeTable:
                nodeTable[val].append(head)
            else:
                nodeTable[val] = [head]
            head = head.next
        valList.sort()
        sortedHead = head = nodeTable[valList[0]].pop()
        for val in valList[1:]:
            head.next = nodeTable[val].pop()
            head = head.next
        head.next  = None
        return sortedHead
```