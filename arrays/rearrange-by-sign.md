---
title: Rearrange Array by Sign
layout: problem
parent: Arrays
nav_order: 5
difficulty: Medium
time: O(n)
space: O(n)
---

`nums` has even length and equal numbers of positives and negatives. Rearrange it so signs alternate, starting with a positive, and each sign keeps its original order.

## Examples

```
Input:  nums = [2, 4, 5, -1, -3, -4]
Output: [2, -1, 4, -3, 5, -4]
```

```
Input:  nums = [1, -1, -3, -4, 2, 3]
Output: [1, -1, 2, -3, 3, -4]
```

{: .intuition }
> **Positives go to the even slots and negatives to the odd slots.** Keep two write pointers, `posIndex = 0` and `negIndex = 1`, each stepping by 2. A single left-to-right scan keeps each sign in its original order.

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ just written</span> · <span class="done">■ filled</span></p>
{% include array.html v="2,4,5,-1,-3,-4" label="nums" note="pos = 0, neg = 1" %}
{% include array.html v="2,_,_,_,_,_" hl="0" label="i = 0" note="2 ≥ 0 → ans[0], pos = 2" %}
{% include array.html v="2,_,4,_,_,_" hl="2" done="0" label="i = 1" note="4 → ans[2], pos = 4" %}
{% include array.html v="2,_,4,_,5,_" hl="4" done="0,2" label="i = 2" note="5 → ans[4], pos = 6" %}
{% include array.html v="2,-1,4,_,5,_" hl="1" done="0,2,4" label="i = 3" note="-1 < 0 → ans[1], neg = 3" %}
{% include array.html v="2,-1,4,-3,5,_" hl="3" done="0,1,2,4" label="i = 4" note="-3 → ans[3], neg = 5" %}
{% include array.html v="2,-1,4,-3,5,-4" hl="5" done="0,1,2,3,4" label="i = 5" note="-4 → ans[5], neg = 7" %}
</div>

## Code

```cpp
class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
      int n = nums.size();
        
        vector<int> ans(n, 0); 
        
        int posIndex = 0, negIndex = 1;  
        
        for (int i = 0; i < n; i++) {
            if (nums[i] < 0) {
                
            
                ans[negIndex] = nums[i];
                
                negIndex += 2;  
                
            } else {
                ans[posIndex] = nums[i];
 
                posIndex += 2;  
            }
        }
        
        return ans;    
    }
};
```

{: .pitfall }
> This only works because the counts are **equal**. If there are more of one sign, `posIndex` or `negIndex` runs past `n` and writes out of bounds. Swapping in place breaks the relative order, so the extra O(n) array is required.

{: .revisit }
> **Variant 2: unequal counts.** Fill `pos[]` and `neg[]` separately. Alternate them for `min(pos, neg)` pairs, then append whatever is left over from the longer list. That is still O(n) time and O(n) space. In both versions, every slot's index is known up front (even or odd), so you write each element directly instead of searching for its place.
