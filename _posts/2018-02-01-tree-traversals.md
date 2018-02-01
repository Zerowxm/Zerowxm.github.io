---
layout: post
title: Tree Traversals (Inorder, Preorder and Postorder)
key: 20180201
tags: leetcode binarytree
---

# Tree Traversals
Tree tavsersals have three different ways: Inorder, Preorder, Postorder. Also there are more compliacted ones like Breadth First Search or A, we focus on the first three ones.
![tree-traversals](http://algorithms.tutorialhorizon.com/tree-traversals/)
This picture shows some intuition. 	
1. Inorder: (Left, Root, Right) 
2. Preorder: (Root, Left, Right)
3. Postorder: (Left, Right, Root) 

Algorithm Inorder(tree)
   1. Traverse the left subtree, i.e., call Inorder(left-subtree)
   2. Visit the root.
   3. Traverse the right subtree, i.e., call Inorder(right-subtree)

Algorithm Preorder(tree)
   1. Visit the root.
   2. Traverse the left subtree, i.e., call Preorder(left-subtree)
   3. Traverse the right subtree, i.e., call Preorder(right-subtree) 

Algorithm Postorder(tree)
   1. Traverse the left subtree, i.e., call Postorder(left-subtree)
   2. Traverse the right subtree, i.e., call Postorder(right-subtree)
   3. Visit the root.

# Implementation
## Inorder
```python
	# iteratively   
	def inorderTraversal(self, root):
	        res, stack = [], []
	        while True:
	            while root:
	                stack.append(root)
	                root = root.left
	            if not stack:
	                return res
	            node = stack.pop()
	            res.append(node.val)
	            root = node.right
	    	# another implimentation using flag
		    res, stack = [], [(root, False)]
	        while stack:
	            cur, visited = stack.pop()
	            if cur:
	                if visited:
	                    res.append(cur.val)
	                else:
	                    stack.append((cur.right, False))
	                    stack.append((cur, True))
	                    stack.append((cur.left, False))

	        return res

	# recursively
	def inorderTraversal(self, root):
	        res = []
	        self.helper(root, res)
	        return res

    def helper(self, root, res):
        if root:
            self.helper(root.left, res)
            res.append(root.val)
            self.helper(root.right, res)
```

## Preorder
```python
	# iteratively   
	def preorderTraversal(self, root):
	        res, stack = [], []
	        while True:
	            while root:
	            	res.append(root)
	            	stack.push(root.right)
	                root = root.left
	            if not stack:
	                return res
	            node = stack.pop()
	            res.append(node.val)
	            root = node.right

	# recursively
	def preorderTraversal(self, root):
	        res = []
	        self.helper(root, res)
	        return res

    def helper(self, root, res):
        if root:
        	res.append(root.val)
            self.helper(root.left, res)
            self.helper(root.right, res)
```

## Postorder
```python
	# iteratively   
	def postorderTraversal(self, root):
		traversal, stack = [], [(root, False)]
        while stack:
            node, visited = stack.pop()
            if node:
                if visited:
                    # add to res if visited
                    traversal.append(node.val)
                else:
                    # post-order
                    stack.append((node, True))
                    stack.append((node.right, False))
                    stack.append((node.left, False))

        return traversal

	# recursively
	def postorderTraversal(self, root):
	        res = []
	        self.helper(root, res)
	        return res

	def helper(self, root, res):
	     if root:
		     self.helper(root.left, res)
		     self.helper(root.right, res)
		     res.append(root.val)
```