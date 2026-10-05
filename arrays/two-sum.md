---
title: Two Sum
parent: Arrays
---

# Two Sum

Given an array and a target, return the indices of the two numbers that add up to the target.

## Approach
Hash map from value to index. For each element, check if `target - x` was already seen.

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> seen;
    for (int i = 0; i < nums.size(); i++) {
        int need = target - nums[i];
        if (seen.count(need)) return {seen[need], i};
        seen[nums[i]] = i;
    }
    return {};
}
```

**Time:** O(n) · **Space:** O(n)
{: .label .label-green }
