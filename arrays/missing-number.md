---
title: Missing Number
layout: problem
parent: Arrays
nav_order: 3
difficulty: Easy
time: O(n)
space: O(1)
---

An array of size `n` holds distinct values from `[0, n]`. Exactly one value is missing. Return it.

## Examples

```
Input:  nums = [0, 2, 3, 1, 4]
Output: 5
```

```
Input:  nums = [0, 1, 2, 4, 5, 6]
Output: 3
```

{: .intuition }
> **Expected total minus actual total.** `0 + 1 + … + n = n(n+1)/2`. Subtract the array's sum and what's left is the missing number.

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ the gap</span></p>
{% include array.html v="0,1,2,4,5,6" hl="3" label="nums" note="N = 6, so the range is 0..6" %}
{% include array.html v="0,1,2,3,4,5,6" hl="3" label="expected" note="sum1 = 6·7/2 = 21" %}
{% include array.html v="0,1,2,4,5,6" label="actual" note="sum2 = 0+1+2+4+5+6 = 18 → 21 − 18 = 3" %}
</div>

## Code

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        
        int N = nums.size();
        
        int sum1 = (N * (N + 1)) / 2;
        
        int sum2 = 0;
        for (int num : nums) {
            sum2 += num;
        }
        
        int missingNum = sum1 - sum2;
        
        return missingNum;
    }
};
```

## Better: XOR (no overflow)

`x ^ x = 0` and `x ^ 0 = x`. XOR every index `0..n` together with every value. Each number that is present shows up twice (once as an index, once as a value) and cancels out. The missing number shows up only once, as an index, so it is what's left.

Start `xr` at `n`, because the loop only covers indices `0..n-1`.

<div class="viz">
<p class="viz-legend"><span class="hl">■ current i</span> · <span class="done">■ already XOR-ed</span></p>
{% include array.html v="0,1,2,4,5,6" label="start" note="xr = N = 6" %}
{% include array.html v="0,1,2,4,5,6" hl="0" label="i = 0" note="6 ^ 0 ^ 0 = 6" %}
{% include array.html v="0,1,2,4,5,6" hl="1" done="0" label="i = 1" note="6 ^ 1 ^ 1 = 6" %}
{% include array.html v="0,1,2,4,5,6" hl="2" done="0,1" label="i = 2" note="6 ^ 2 ^ 2 = 6" %}
{% include array.html v="0,1,2,4,5,6" hl="3" done="0,1,2" label="i = 3" note="6 ^ 3 ^ 4 = 1 (mismatch starts)" %}
{% include array.html v="0,1,2,4,5,6" hl="4" done="0,1,2,3" label="i = 4" note="1 ^ 4 ^ 5 = 0" %}
{% include array.html v="0,1,2,4,5,6" hl="5" done="0,1,2,3,4" label="i = 5" note="0 ^ 5 ^ 6 = 3 → answer" %}
</div>

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int N = nums.size();
        int xr = N;                 // index N has no slot in the loop
        for (int i = 0; i < N; i++)
            xr ^= i ^ nums[i];      // present numbers cancel in pairs
        return xr;
    }
};
```

{: .pitfall }
> `N * (N + 1)` is an `int` and overflows once `N` passes about 46,000. Signed overflow is undefined behavior in C++. Use `long long`, or use XOR, which can never overflow.

{: .revisit }
> Both are O(n) time and O(1) space. XOR wins because it can't overflow. Remember the trick: **a ^ a = 0, so pairs cancel and the odd one out survives.** The same idea solves "Single Number". Sorting (O(n log n)) or a hash set (O(n) space) also work but are worse.
