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

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ key, after inserting</span> · <span class="done">■ sorted left part</span></p>
{% include array.html v="7,4,1,5,3" done="0" label="start" note="[7] alone is sorted" %}
{% include array.html v="4,7,1,5,3" hl="0" done="1" label="i = 1" note="key 4: shift 7 → insert at 0" %}
{% include array.html v="1,4,7,5,3" hl="0" done="1,2" label="i = 2" note="key 1: shift 7, 4 → insert at 0" %}
{% include array.html v="1,4,5,7,3" hl="2" done="0,1,3" label="i = 3" note="key 5: shift 7, stop at 4 → insert at 2" %}
{% include array.html v="1,3,4,5,7" hl="1" done="0,2,3,4" label="i = 4" note="key 3: shift 7, 5, 4 → insert at 1" %}
</div>

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
