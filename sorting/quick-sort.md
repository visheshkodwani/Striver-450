---
title: Quick Sort
layout: problem
parent: Sorting
nav_order: 4
difficulty: Medium
time: O(n log n) avg, O(n²) worst
space: O(log n) stack
---

Sort an array of integers in non-decreasing order using quick sort.

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
> **Pick a pivot, put it in its final spot, recurse on both sides.** Partition with the last element as pivot: `i` marks the end of the "smaller than pivot" zone. Every `nums[j] < pivot` is swapped into that zone. Finally swap the pivot to `i + 1`. Everything left of it is smaller, everything right is bigger or equal.

## Code

```cpp
class Solution {
public:
int partition(vector<int>& nums, int start , int end){
    int pivot = end;
    int i = start-1;
    for (int j = start ; j<=end-1;j++){
        if(nums[j] < nums[pivot])
        {
            i++;
            swap(nums[i],nums[j]);

        }
    }
    i++;
    swap(nums[i],nums[end]);
    return i;
}
 void quickSortHelper(vector<int>& nums, int start, int end) {
    
        if (start < end) {
            int pivot = partition(nums, start, end);
            quickSortHelper(nums, start, pivot - 1);
            quickSortHelper(nums, pivot + 1, end);
        }
    }
    vector<int> quickSort(vector<int>& nums) {
        int start = 0 ;
        int end = nums.size()-1;
        quickSortHelper(nums, start, end);
    return nums;


    }
  
};
```

{: .pitfall }
> Recurse on `pivot - 1` and `pivot + 1`, never include the pivot again or it loops forever. With the last element as pivot, an already-sorted array hits the O(n²) worst case.

## Better: random pivot

Swap a random element to `end` before partitioning. No fixed input (like a sorted array) can force O(n²) anymore; expected time is O(n log n). Only `partition` changes.

```cpp
int partition(vector<int>& nums, int start, int end) {
    swap(nums[start + rand() % (end - start + 1)], nums[end]);  // random pivot to end
    int i = start - 1;
    for (int j = start; j < end; j++)
        if (nums[j] < nums[end]) swap(nums[++i], nums[j]);
    swap(nums[++i], nums[end]);
    return i;
}
```

{: .revisit }
> Quick sort is in-place but not stable. Many equal elements still cause O(n²) with this partition; a 3-way partition (`<`, `==`, `>` pivot) fixes that. In practice, `sort()` from `<algorithm>` is the answer.
