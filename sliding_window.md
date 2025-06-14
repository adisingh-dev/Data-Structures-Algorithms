
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
- [Smallest distinct window](https://www.geeksforgeeks.org/problems/smallest-distant-window3132/1?page=1&category=sliding-window&sortBy=submissions)

## Thinking Patterns
-  For problem Longest substring with distinct characters know when to use either hashmap or integer array of some size. know how and when to move `i` pointer efficiently.
move `i` only when a char is found whose first occuring idx `arr[s[j]] >= i` before updating hash array but dont update i when `arr[idx] < i` bcoz `i` already passed by `s[j]`
element hence no need to update `i`
    ```cpp
    if(arr[s[j] - 'a'] != -1 && arr[s[j] - 'a'] >= i) {
        i = arr[s[j] - 'a'] + 1;
    }
    ```
- For problem Max Consecutive Ones III there is 1 better and 1 optimal technique we can use
    -  __better__: use while loop. increment `i` one by one till it reaches a pt where #of zeros are valid
    ```cpp
    if(arr[j] == 0) z++;
    while(i <= j && z > k) {
        if(arr[i] == 0) z--;
        i++;
    }
    ```
    -  __optimal__: use if condition and increment `i` by one idx. this ensures we only get `length >= current length` as there is no point in shrinking `i` for lower lengths
    ```cpp
    if(z > k) {
        if(arr[i] == 0) z--;
        i++;
    }
    if(z <= k) mx = max(mx, j - i + 1); // optional check
    // we are not allowing maxlength to be greater than the current one so
    // even if current subarray is invalid still we get current subarray length to be equal
    // to maxlength so it dont make a difference
    ```
- In problem Smallest distinct window we need to find length of the smallest window that contains all the characters
  of the given string at least once. To tackle it think of a frequency array and a counter variable `c` instead of using
  2 hashmaps
    - Initialize freq array w/ -1 and put 0 count for all occuring chars in string s
    - If the char occurs first time increase counter variable by 1 by using `if(freq[i]] == -1)`
    - Decrement counter by one only when the character occurs once inside while loop
    - shrink window size till we are able to have a valid window by checking `if(i <= j && c == 0)` which means all chars are consumed
      ```cpp
      while(j<str.size()){
            a[str[j]-'a']++;
            if(a[str[j]-'a']==1){
                c--;
            }
            while(i<=j&&c==0){
                mn=min(mn,j-i+1);
                a[str[i]-'a']--;
                if(a[str[i]-'a']==0){
                    c++;
                }
                i++;
            }
            j++;
        }
      ```
