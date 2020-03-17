# Chapter 1: Lists and Strings

## 1.1 Dictionary Storage

### 1.1.1 Two Sum
Given an array of integers, return the indices of two numbers that add up to a specific target. You may assume each input has only one solution. You may not use the same element twice.
```
Example
nums = [2, 7, 11, 15], target = 9
nums[0] + nums[1] = 2 + 7 = 9
so return [0, 1]
```
Sources: LC 1

Solution
```Python
def twoSum(nums, target):
	d = {}
	for i, e in enumerate(nums):
		if target - e in d:
			return [d[target - e], i]
		d[e] = i
	return []
```
