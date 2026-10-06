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

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ swapped</span> · <span class="done">■ final</span></p>
{% include array.html v="7,4,1,5,3" label="start" %}
{% include array.html v="1,4,7,5,3" hl="0,2" label="i = 0" note="min of [0..4] is 1 at idx 2 → swap with idx 0" %}
{% include array.html v="1,3,7,5,4" hl="1,4" done="0" label="i = 1" note="min of [1..4] is 3 at idx 4 → swap with idx 1" %}
{% include array.html v="1,3,4,5,7" hl="2,4" done="0,1" label="i = 2" note="min of [2..4] is 4 at idx 4 → swap with idx 2" %}
{% include array.html v="1,3,4,5,7" hl="3" done="0,1,2" label="i = 3" note="min of [3..4] is 5, already in place" %}
{% include array.html v="1,3,4,5,7" done="0,1,2,3,4" label="done" %}
</div>

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
