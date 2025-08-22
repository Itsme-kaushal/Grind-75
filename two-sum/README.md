# Two Sum Problem

## Problem Statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

### Example 3:
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

### Constraints:
- 2 <= nums.length <= 10^4
- -10^9 <= nums[i] <= 10^9
- -10^9 <= target <= 10^9
- Only one valid answer exists.

## Approach

The optimal solution uses a hash map (dictionary) to store the numbers we've seen and their indices. As we iterate through the array:

1. For each number, calculate its complement (target - current number)
2. Check if the complement exists in our hash map
3. If it exists, we found our pair - return the indices
4. If not, store the current number and its index in the hash map
5. Continue until we find the solution

**Time Complexity:** O(n) - We traverse the list containing n elements only once
**Space Complexity:** O(n) - The extra space required depends on the number of items stored in the hash table

## Python Solution

```python
def twoSum(nums, target):
    """
    :type nums: List[int]
    :type target: int
    :rtype: List[int]
    """
    # Dictionary to store number and its index
    num_map = {}
    
    # Iterate through the array
    for i, num in enumerate(nums):
        # Calculate complement
        complement = target - num
        
        # Check if complement exists in our map
        if complement in num_map:
            # Return indices of complement and current number
            return [num_map[complement], i]
        
        # Store current number and its index
        num_map[num] = i
    
    # This should never be reached given problem constraints
    return []

# Test cases
if __name__ == "__main__":
    # Test case 1
    nums1 = [2, 7, 11, 15]
    target1 = 9
    print(f"Input: nums = {nums1}, target = {target1}")
    print(f"Output: {twoSum(nums1, target1)}")
    print()
    
    # Test case 2
    nums2 = [3, 2, 4]
    target2 = 6
    print(f"Input: nums = {nums2}, target = {target2}")
    print(f"Output: {twoSum(nums2, target2)}")
    print()
    
    # Test case 3
    nums3 = [3, 3]
    target3 = 6
    print(f"Input: nums = {nums3}, target = {target3}")
    print(f"Output: {twoSum(nums3, target3)}")
```