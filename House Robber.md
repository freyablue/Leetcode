### Dynamic Programming
198. House Robber(Medium)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

The core is: d[i] = max(d[i-2]+nums[i-1],d[i-1])
````
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        d = {}
        if n==1:
            return nums[0]
        if n==2:
            return max(nums[0],nums[1])
        if n>=3:
            d[1], d[2] = nums[0], max(nums[0],nums[1])
            for i in range(3,n+1):
                d[i] = max(d[i-2]+nums[i-1],d[i-1])
        return d[n]
                
 ````
 213. House Robber II
 
 All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.
````
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)
        if n==1:
            return nums[0]
        if n==2:
            return max(nums[0],nums[1])
        return max(self.helper(0, n-2, nums), self.helper(1,n-1,nums))               
    def helper(self, start, end, nums):
        pre2 = 0
        pre1 = 0
        for i in range(start,end+1):
            cur = max(pre1, pre2 + nums[i])
            pre2 = pre1
            pre1 = cur    
        return pre1
````
337. House Robber III

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root.

Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night.

Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police.

````
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rob(self, root: TreeNode) -> int:
        return max(self.dfs(root))
    
    def dfs(self, root: TreeNode):
        if root == None:
            return (0, 0)
        l = self.dfs(root.left)
        # print(root)
        r = self.dfs(root.right)
        return (root.val + l[1] + r[1], max(l[0], l[1]) + max(r[0], r[1]))

"""
    Input: [3,4,5,1,3,null,1]
 input tree            dp tree:
     3                  [3+3+1,4+5]
    / \                /        \
   4   5            [4,3]      [5,1]
  / \   \          /     \          \
 1   2   1      [1,0]    [2,0]     [1,0]
                / \       /  \        /  \
           [0,0] [0,0] [0,0] [0,0]  [0,0] [0,0]
    
"""        
