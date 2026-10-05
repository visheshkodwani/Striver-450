---
title: Two Sum
layout: problem
parent: Arrays
nav_order: 1
difficulty: Easy
time: O(n)
space: O(n)
link: https://leetcode.com/problems/two-sum/
---

Given an array and a target, return the indices of the two numbers that add up to the target.

{: .intuition }
> For each number `x`, the partner we need is `target - x`. If we have already seen it, we are done. A hash map makes that lookup O(1).

## Code

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> seen;  // value -> index
    for (int i = 0; i < nums.size(); i++) {
        int need = target - nums[i];
        if (seen.count(need)) return {seen[need], i};
        seen[nums[i]] = i;
    }
    return {};
}
```

{: .pitfall }
> Insert `nums[i]` **after** checking, otherwise `x + x = target` matches the same element twice.

{: .revisit }
> Brute force is O(n²). If the array were sorted, two pointers would do it in O(1) space.
