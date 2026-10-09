---
title: Majority Element
layout: problem
parent: Arrays
nav_order: 6
difficulty: Easy
time: O(n)
space: O(1)
---

Return the element that appears more than `n/2` times. A majority element is guaranteed to exist.

## Examples

```
Input:  nums = [7, 0, 0, 1, 7, 7, 2, 7, 7]
Output: 7
```

{: .intuition }
> **Moore's Voting: every non-majority element can cancel at most one majority vote.** Keep a candidate `res` and a `count`. A match adds 1 and a mismatch subtracts 1. When `count` drops to 0, take the current element as the new candidate. The majority has more than n/2 copies, so it outnumbers all the others combined and is the candidate left at the end.

## Dry run

<div class="viz">
<p class="viz-legend"><span class="hl">■ current i</span></p>
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="0" label="i = 0" note="count 0 → res = 7, count = 1" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="1" label="i = 1" note="0 ≠ 7 → count = 0" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="2" label="i = 2" note="count 0 → res = 0, count = 1" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="3" label="i = 3" note="1 ≠ 0 → count = 0" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="4" label="i = 4" note="count 0 → res = 7, count = 1" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="5" label="i = 5" note="7 = 7 → count = 2" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="6" label="i = 6" note="2 ≠ 7 → count = 1" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="7" label="i = 7" note="7 = 7 → count = 2" %}
{% include array.html v="7,0,0,1,7,7,2,7,7" hl="8" label="i = 8" note="7 = 7 → count = 3 → answer 7" %}
</div>

## Code

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res ;
        int count = 0;
        for (int i = 0; i< nums.size();i++){
            if(count == 0)
            {
            res = nums[i];
            count++;
            }
            else if (res == nums[i])
            count++;
            else if (res != nums[i])
            count--;
        }
        return res;
        
    }
};
```

{: .pitfall }
> The final `res` is only *a candidate*. It is correct here only because a majority is guaranteed. If it might not exist, run a second pass that counts `res` and checks `count > n/2`. On `[1, 2, 3]`, for example, the vote returns 3, which is not a majority.

{: .revisit }
> Other approaches: a hash map of counts is O(n) time and O(n) space. Sorting and returning `nums[n/2]` is O(n log n). Moore beats both at O(n) time and O(1) space. **Majority Element II (> n/3)** uses the same trick with two candidates and two counts, then a verify pass.
