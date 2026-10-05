---
title: Insertion Sort
layout: problem
parent: Sorting
nav_order: 3
difficulty: Easy
time: O(n²)
space: O(1)
---

Sort an array of integers in non-decreasing order using insertion sort.

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
> **Take the next element and insert it into its place in the sorted left part.** Keep `nums[0..i-1]` sorted. Pick `key = nums[i]`, shift every bigger element one step right, then drop `key` into the gap.

## Code

```cpp
class Solution {
public:
    vector<int> insertionSort(vector<int>& nums) {
        for (int i = 1 ; i < nums.size();i++){
            int key = nums[i];
            int j = i-1;
            while(j>=0 && nums[j] > key)
            {
                nums[j+1]=nums[j];
                j--;
            }
            nums[j+1]=key;
        }
        return nums;

    }
};
```

{: .pitfall }
> Save `nums[i]` in `key` before shifting, because the first shift overwrites it. Check `j >= 0` before `nums[j]`, otherwise you read out of bounds.

{: .revisit }
> Best case O(n) on an already-sorted array (the while loop never runs), so it is great for nearly sorted data. It is stable because of the strict `>`.
