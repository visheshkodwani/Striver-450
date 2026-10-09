---
title: Leaders in an Array
layout: problem
parent: Arrays
nav_order: 4
difficulty: Easy
time: O(n)
space: O(1)
---

Return every element that is strictly greater than all elements to its right, in their original order. The rightmost element is always a leader.

## Examples

```
Input:  nums = [1, 2, 5, 3, 1, 2]
Output: [5, 3, 2]
```

```
Input:  nums = [-3, 4, 5, 1, -4, -5]
Output: [5, 1, -4, -5]
```

{: .intuition }
> **Scan from the right and keep the max seen so far.** An element is a leader if it beats that max. Leaders get pushed in increasing order, so `ans.back()` *is* the running max. Reverse at the end to restore the left-to-right order.

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ current i</span> · <span class="done">■ leader</span></p>
{% include array.html v="1,2,5,3,1,2" done="5" label="start" note="push 2 → ans = [2]" %}
{% include array.html v="1,2,5,3,1,2" hl="4" done="5" label="i = 4" note="1 > 2? no" %}
{% include array.html v="1,2,5,3,1,2" hl="3" done="5" label="i = 3" note="3 > 2? yes → ans = [2, 3]" %}
{% include array.html v="1,2,5,3,1,2" hl="2" done="3,5" label="i = 2" note="5 > 3? yes → ans = [2, 3, 5]" %}
{% include array.html v="1,2,5,3,1,2" hl="1" done="2,3,5" label="i = 1" note="2 > 5? no" %}
{% include array.html v="1,2,5,3,1,2" hl="0" done="2,3,5" label="i = 0" note="1 > 5? no" %}
{% include array.html v="5,3,2" done="0,1,2" label="reverse" note="ans = [5, 3, 2]" %}
</div>

## Code

```cpp
class Solution {
public:
    vector<int> leaders(vector<int>& nums) {
        vector<int> ans;
        ans.push_back(nums[nums.size()-1]);
        for (int i=nums.size()-2;i>=0;i--){
            if(nums[i] > ans[ans.size()-1])
            ans.push_back(nums[i]);
        }
        reverse(ans.begin(),ans.end());
        return ans;
      
    }
};
```

{: .pitfall }
> Use **strictly** greater, `>`. With `>=`, the input `[2, 2]` would wrongly return both 2s. An empty `nums` crashes: `nums.size()-1` is unsigned and wraps to a huge index. Return `{}` early if the input can be empty.

{: .revisit }
> Brute force checks every element against everything on its right, O(n²). Going right-to-left with a running max gives O(n). Space is O(1) besides the output. "Compare against everything to the right" → **scan from the right**. The same idea gives suffix-max arrays and Best Time to Buy and Sell Stock.
