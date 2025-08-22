# Two Sum Problem

## Problem Statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

### Example 2:

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]

### Example 3:

**Input:** nums = [3,3], target = 6
**Output:** [0,1]

### Constraints:

- 2 <= nums.length <= 10^4
- -10^9 <= nums[i] <= 10^9
- -10^9 <= target <= 10^9
- Only one valid answer exists.

**Follow-up:** Can you come up with an algorithm that is less than O(n²) time complexity?

## Approach

### Hash Map Approach (Optimal Solution)

**Time Complexity:** O(n)
**Space Complexity:** O(n)

The most efficient approach uses a hash map to store the numbers we've seen so far and their indices. For each number, we check if its complement (target - current number) exists in the hash map.

**Algorithm:**
1. Initialize an empty hash map
2. Iterate through the array
3. For each element, calculate its complement (target - current element)
4. Check if the complement exists in the hash map
5. If it exists, return the indices
6. If not, add the current element and its index to the hash map
7. Continue until we find the solution

## C++ Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> numMap; // value -> index
        
        for (int i = 0; i < nums.size(); i++) {
            int complement = target - nums[i];
            
            // Check if complement exists in the map
            if (numMap.find(complement) != numMap.end()) {
                return {numMap[complement], i};
            }
            
            // Add current number and its index to the map
            numMap[nums[i]] = i;
        }
        
        // Should never reach here based on problem constraints
        return {};
    }
};
```

### Alternative Approaches

#### Brute Force Approach
**Time Complexity:** O(n²)
**Space Complexity:** O(1)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] + nums[j] == target) {
                    return {i, j};
                }
            }
        }
        return {};
    }
};
```

## Key Insights

1. **Hash Map Trade-off:** We trade space for time complexity, using O(n) extra space to achieve O(n) time complexity.

2. **Single Pass:** The optimal solution only requires one pass through the array.

3. **Early Termination:** We can return as soon as we find the first valid pair.

4. **Complement Logic:** Instead of checking all pairs, we only need to check if the complement of the current number exists.

## Test Cases

```cpp
// Test Case 1
vector<int> nums1 = {2, 7, 11, 15};
int target1 = 9;
// Expected: [0, 1]

// Test Case 2
vector<int> nums2 = {3, 2, 4};
int target2 = 6;
// Expected: [1, 2]

// Test Case 3
vector<int> nums3 = {3, 3};
int target3 = 6;
// Expected: [0, 1]
```