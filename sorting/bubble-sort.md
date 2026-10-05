---
title: Bubble Sort
layout: problem
parent: Sorting
nav_order: 2
difficulty: Easy
time: O(n²)
space: O(1)
---

Sort an array of integers in non-decreasing order using bubble sort.

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
> **Reverse of selection sort: push the max to the end using adjacent swaps.** In each pass, compare neighbours and swap if out of order, so the largest element bubbles to the last unsorted spot. After pass `i`, the last `i + 1` elements are sorted and final.

## Code

```cpp
class Solution {
public:
    vector<int> bubbleSort(vector<int>& nums) {
        for (int i = 0 ; i < nums.size();i++){
            for (int j = 0 ; j < nums.size()-i-1;j++){
                if(nums[j]>nums[j+1])
                swap(nums[j],nums[j+1]);
            }
        }
        return nums;

    }
};
```

{: .pitfall }
> The inner loop stops at `n - i - 1` because `j + 1` must stay in bounds and the last `i` elements are already in place.

{: .revisit }
> Add a `bool swapped` flag and break when a pass makes no swaps: a sorted array then takes O(n). Bubble sort is stable, selection sort is not.
