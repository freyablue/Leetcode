#### 55. Jump Game(Medium)

Discussion Idea:
Base case: last index can trivially reach to last index.
Q1: How can I reach to the last index (I will call it last_position) from a preceding index?
If I have a preceding index idx in nums which has jump count jump which satisfies idx+jump >= last_position, I know that this idx is good enough to be treated as the last index because all I need to do now is to get to that idx. I am going to treat this new idx as a new last_position.
I ask Q1 again.

````
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)-1
        last_pos = n
        while n>=0:
            if last_pos==0:
                return True
            if n-1>=0:
                if nums[n-1]+n-1>=last_pos:
                    last_pos = n-1
            n-=1
        return False
````
#### 343. Integer Break (Medim)

Given an integer n, break it into the sum of k positive integers, where k >= 2, and maximize the product of those integers.

Return the maximum product you can get.

 

Example 1:

Input: n = 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
Example 2:

Input: n = 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.

````
class Solution:
    def integerBreak(self, n: int) -> int:
        d = [0]*(n+1)
        com = 0
        if n<=1:
            return 0
        for i in range(2,n+1):
            for j in range(1,i):
                com = max(d[i-j]*j,(i-j)*j)
                d[i] = max(d[i],com)
        return d[n]
````
