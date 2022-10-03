#### 104. Maximum Depth of Binary Tree (Easy)

Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

````
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root: return 0
        result = 0
        if root.val!= None:
            result = result + 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
        return result
            
````

#### 110. Balanced Binary Tree (Easy)

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

````
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True
        
        def height(root):
            if not root:
                return 0
            return 1+ max(height(root.left), height(root.right))        
        l = height(root.left)
        r = height(root.right)
        if abs(l-r)>1:
            return False
        return (self.isBalanced(root.left) and self.isBalanced(root.right))
````
#### 543. Diameter of Binary Tree (Easy)

Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.

````
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        s = {'max':0}
        if not root:
            return 0
        def height(root):
            if not root:
                return 0
            l = height(root.left)
            r = height(root.right)
            s['max'] = max(s['max'], l+r)
            return 1+ max(l,r)   
        height(root)
        return s['max']

````
