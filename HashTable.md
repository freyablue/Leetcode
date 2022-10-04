#### 594. Longest Harmonious Subsequence (Easy)

We define a harmonious array as an array where the difference between its maximum value and its minimum value is exactly 1.

Given an integer array nums, return the length of its longest harmonious subsequence among all its possible subsequences.

A subsequence of array is a sequence that can be derived from the array by deleting some or no elements without changing the order of the remaining elements.

````
Input: nums = [1,1,1,1]
Output: 0

Input: nums = [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].
````
>>> from collections import Counter
>>> 
>>> myList = [1,1,2,3,4,5,3,2,3,4,2,1,2,3]
>>> print Counter(myList)
Counter({2: 4, 3: 4, 1: 3, 4: 2, 5: 1})

Counter in python3 can do what my dictionary does

````
class Solution:
    def findLHS(self, nums: List[int]) -> int:
        if len(nums)<=1: return 0
        d = dict()
        for item in set(nums):
            d[item] = 0
        for num in nums:
            d[num]+=1
        c = 0
        for k in d.keys():
            if k+1 in d.keys():
                    c = max(c,d[k]+d[k+1])
        return c
````
