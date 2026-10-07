---
title: Move Zeroes
layout: problem
parent: Arrays
nav_order: 2
difficulty: Easy
time: O(n)
space: O(1)
---

Move all the 0's in `nums` to the end, in place, keeping the relative order of the non-zero elements.

## Examples

```
Input:  nums = [0, 1, 4, 0, 5, 2]
Output: [1, 4, 5, 2, 0, 0]
```

```
Input:  nums = [0, 0, 0, 1, 3, -2]
Output: [1, 3, -2, 0, 0, 0]
```

{: .intuition }
> **`nzi` is where the next non-zero goes.** Scan with `i`; every non-zero gets swapped to `nums[nzi]` and `nzi++`. Everything left of `nzi` is the non-zeros in order, and the zeros get pushed right by the swaps.

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ swapped</span> · <span class="done">■ placed (index &lt; nzi)</span></p>
{% include array.html v="0,1,4,0,5,2" label="start" note="nzi = 0" %}
{% include array.html v="0,1,4,0,5,2" label="i = 0" note="0 → skip, nzi = 0" %}
{% include array.html v="1,0,4,0,5,2" hl="0,1" label="i = 1" note="1: swap(0, 1) → nzi = 1" %}
{% include array.html v="1,4,0,0,5,2" hl="1,2" done="0" label="i = 2" note="4: swap(1, 2) → nzi = 2" %}
{% include array.html v="1,4,0,0,5,2" done="0,1" label="i = 3" note="0 → skip, nzi = 2" %}
{% include array.html v="1,4,5,0,0,2" hl="2,4" done="0,1" label="i = 4" note="5: swap(2, 4) → nzi = 3" %}
{% include array.html v="1,4,5,2,0,0" hl="3,5" done="0,1,2" label="i = 5" note="2: swap(3, 5) → nzi = 4" %}
{% include array.html v="1,4,5,2,0,0" done="0,1,2,3" label="end" note="non-zeros in order, zeros at the end" %}
</div>

## Code

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int nzi = 0;
        for (int i = 0 ; i < nums.size();i++){
            if (nums[i] != 0)
            {
                swap(nums[nzi],nums[i]);
                nzi++;
            }
        }
        
    }
};
```

{: .pitfall }
> Swap, don't just copy. `nums[nzi] = nums[i]` leaves the old values behind, so you need a second loop to fill zeros from `nzi` to the end. The swap does both in one pass.

{: .revisit }
> Same two-pointer "write index" pattern as Remove Duplicates from Sorted Array and the partition step in Quick Sort. Order is kept because `nzi <= i` always, so non-zeros only ever move left in scan order.
