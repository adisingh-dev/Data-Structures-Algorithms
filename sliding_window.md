
# Sliding Window

## Concept
It is a constructive algorithm. that requires two pointer technique. This technique has to be mould according to the problem statement based on a condition. It requires 2 pointers `left` and `right` and is based on the concept of expanding and shrinking the window size. *__window shrinks for `left` pointer and expands for `right` pointer__*


## Types
* `fixed size`
* `variable size`
    - In this type of sliding window problem, we increase our     right pointer one by one till our condition is true.
    - At any step if our condition does not match, we shrink the size of our window by increasing left pointer.
    - Again, when our condition satisfies, we start increasing the right pointer and follow step 1.

## Patterns
#### 1. Fixed size
#### 2. Longest subarray/substring where <condition>
- eg. longest subarray with sum <= k
```cpp
** brute force **
TC: O(n^2)
SC: O(1)

mx = MIN
for(i = 0 => n - 1) {
    sum = 0
    for(j = i => n - 1) {
        sum += arr[j]
        if(sum <= k) mx = max(mx, j - i + 1)
        else if(sum > k) break // optimization
    }
}
return mx
```

```cpp
** Better **
TC: O(2n)
SC: O(1)

int i = 0, j = 0, sum = 0
while(j < n) {
    sum += arr[j]
    while(i <= j and sum > k) {
        sum = sum - arr[i]
        i++
    }
    if(sum <= k) mx = max(mx, j - i + 1)
    j++
}
return mx
```

```cpp
** Optimal **
The idea is to trim down the shrinking part as we already have an optimal solution in variable mx. so we dont need a
length <= mx so far. so we shrink the window size by 1 by converting while loop to if chk and see if we can obtain a
window whose size is greater than current mx

TC: O(n)
SC: O(1)
...
if(i <= j and sum > k) { // chk only for window size > mx
    sum = sum - arr[i]
    i++
}
...
```

#### 3. No. of subarrays/substrings where <condition>
- these are difficult to solve as it is tough to find out all the subarrays satisfying the condition
- these problems are solved using `pattern-2`
```cpp
# of subarrays with sum == k => N
N = solve(arr, k) - solve(arr, k - 1);
N = (# of subarrays with sum <= k) - (# of subarrays with sum <= k - 1)
```

#### Revision
- [Longest substring with distinct characters](https://www.geeksforgeeks.org/problems/longest-distinct-characters-in-string5848/1?page=1&sprint=cd7efdc1e9a023839c3b9c0155ad1d7c&sortBy=submissions)
- [Binary subarray with sum](https://www.geeksforgeeks.org/problems/binary-subarray-with-sum/1?page=1&sprint=7bf27b675324d23aa478f42454c72fa6&sortBy=submissions)
- [Fruit Into Baskets](https://takeuforward.org/plus/dsa/problems/fruit-into-baskets)
- [Number of substring containing all three characters](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/description/)
- [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/description/)
- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/description/)
- [Minimum Window Substring](https://www.geeksforgeeks.org/problems/minimum-window-subsequence/1)
- [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/description/)
- [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
