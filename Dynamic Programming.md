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
