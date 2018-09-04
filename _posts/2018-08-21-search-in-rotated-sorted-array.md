---
layout: post
title: Leetcode 33. Search in Rotated Sorted Array Review
date: 2018-08-21
---

This problem was a doozy! It's a medium difficulty problem with a 32% correct submission rate. This is a spin off binary search, with a few extra conditions due to the rotations. I'm posting this one, because it took a me a while to figure out.
<!--break-->

My edge cases were on the bounds on low and high - I had to check if they were greater than or equal to these values.

```python
class Solution(object):
    def searchHelper(self, nums, target, low_idx, high_idx):
        if not nums:  #case 0: there is no elements in nums
            return -1
        
        if low_idx > high_idx: #if the pointers have passed each other, not in the array
            return -1
        
        mid_idx = (high_idx + low_idx) // 2
        
        if nums[mid_idx] == target:
            return mid_idx
        
        if (nums[mid_idx] > nums[high_idx]): # pivot is on RHS
            if target >= nums[low_idx] and target <= nums[mid_idx]: #if it's in the range of the LHS
                return self.searchHelper(nums, target, low_idx, mid_idx-1) #check the LHS
            else:
                return self.searchHelper(nums, target, mid_idx+1, high_idx) #check the RHS
        
        if (nums[low_idx] > nums[mid_idx]): # pivot is on LHS
            if target >= nums[mid_idx] and target <= nums[high_idx]:  #if it's in the range of the RHS
                return self.searchHelper(nums, target, mid_idx+1, high_idx) # check the RHS
            else:
                return self.searchHelper(nums, target, low_idx, mid_idx-1) # check the LHS
        
        # General binary search cases
        if nums[mid_idx] < target:
            return self.searchHelper(nums, target, mid_idx+1, high_idx)
        
        if nums[mid_idx] > target:
            return self.searchHelper(nums, target, low_idx, mid_idx-1)
        
        
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: bool
        """
        return self.searchHelper(nums, target, 0, len(nums)-1)
        ```