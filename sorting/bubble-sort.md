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

## Dry run

Pass 1 step by step: watch 7 bubble to the end.

<div class="viz">
<p class="viz-legend"><span class="hl">■ compared</span> · <span class="done">■ final</span></p>
{% include array.html v="7,4,1,5,3" label="start" %}
{% include array.html v="4,7,1,5,3" hl="0,1" label="j = 0" note="7 > 4 → swap" %}
{% include array.html v="4,1,7,5,3" hl="1,2" label="j = 1" note="7 > 1 → swap" %}
{% include array.html v="4,1,5,7,3" hl="2,3" label="j = 2" note="7 > 5 → swap" %}
{% include array.html v="4,1,5,3,7" hl="3,4" label="j = 3" note="7 > 3 → swap, 7 is final" %}
</div>

End of each pass:

<div class="viz">
{% include array.html v="4,1,5,3,7" done="4" label="pass 1" note="7 bubbled to idx 4" %}
{% include array.html v="1,4,3,5,7" done="3,4" label="pass 2" note="5 bubbled to idx 3" %}
{% include array.html v="1,3,4,5,7" done="2,3,4" label="pass 3" note="4 bubbled to idx 2" %}
{% include array.html v="1,3,4,5,7" done="0,1,2,3,4" label="pass 4" note="no swaps → sorted (the better version stops here)" %}
</div>

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

## Better: stop early

If a whole pass makes no swaps, the array is already sorted. A sorted input now takes O(n) instead of O(n²).

```cpp
vector<int> bubbleSort(vector<int>& nums) {
    int n = nums.size();
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (nums[j] > nums[j + 1]) {
                swap(nums[j], nums[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;  // no swaps = already sorted
    }
    return nums;
}
```

{: .revisit }
> Bubble sort is stable, selection sort is not. Best case O(n) only with the `swapped` flag.
