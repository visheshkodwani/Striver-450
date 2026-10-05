---
title: Selection Sort
layout: problem
parent: Sorting
nav_order: 1
difficulty: Easy
time: O(n²)
space: O(1)
---

Sort an array of integers in non-decreasing order using selection sort.

## Examples

```
Input:  nums = [7, 4, 1, 5, 3]
Output: [1, 3, 4, 5, 7]
```

```
Input:  nums = [5, 4, 4, 1, 1]
Output: [1, 1, 4, 4, 5]
```

{: .intuition }
> **Select the minimum, then swap.** For each position `i`, find the smallest element in `nums[i..n-1]` and swap it into `nums[i]`. After pass `i`, the prefix `nums[0..i]` is sorted and final.

## Code

```cpp
class Solution {
   public:
    vector<int> selectionSort(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++) {
            int minelement = INT_MAX;
            int minIndex;
            for (int j = i; j < nums.size(); j++) {
                if (nums[j] < minelement) {
                    minelement = nums[j];
                    minIndex = j;
                }
            }
            swap(nums[i], nums[minIndex]);
        }
        return nums;
    }
};
```

{: .pitfall }
> `minIndex` is never initialized. It works because `j` starts at `i`, so the first comparison always sets it. Writing `int minIndex = i;` is safer, and then `minelement` isn't needed at all: compare against `nums[minIndex]`.

{: .revisit }
> Always O(n²) comparisons, even on a sorted array. It does at most n-1 swaps, which is the fewest of the simple sorts. It is not stable.
