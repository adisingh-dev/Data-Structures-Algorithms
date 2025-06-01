
# Recursion-Backtracking

## Patterns
#### 1. For combinatorial style problems think in terms of pick and not pick like in subsequence sum equal target
#### 2. To print all combinations: use functional params and reduce `target` till we hit base case
#### 3. To print any one combination: return  `true/false` and avoid recursion calls if get true
#### 4. To count all combinations: calculate the results of all possible options eg. `left & right recursive calls` then 
  `return l + r`

## Thinking Patterns
- For finding `sum = target` always make sure to `return/break` whenever `current sum > target` to avoid unnecessary calls
    ```cpp
    // for combination sum 2
    for(int i = ind; i < arr.size(); i++) {
          if(i > ind && arr[i] == arr[i - 1]) continue; // pick repeated elements only while starting the loop
          if(target - arr[i] < 0) return; // break when sum exceeds target
          v.push_back(arr[i]);
          f(arr, ans, v, target - arr[i], i + 1);
          v.pop_back();
      }
    ```

- For combination sum pattern where all array elems are unique and we are to `find all unique combinations in the array where
  sum equal to target` then use either two recursive calls to find valid combinations using pick/not-pick approach or use a single
  for loop to explore all possible options at once instead of direct pick/not-pick approach
  
  ![WhatsApp Image 2025-06-01 at 18 55 32](https://github.com/user-attachments/assets/53c33f62-d5ca-4723-9efd-2dd4b3fb51b3)

  ```cpp
  // pick/not-pick
  if(sum + arr[ind] <= tar) {
      temp.push_back(arr[ind]);
      f(arr, ans, temp, tar, sum + arr[ind], ind);
      temp.pop_back();
  }
  f(arr, ans, temp, tar, sum, ind + 1);

  // explore all possible options at one level of recursive call
  for(int i = ind; i < arr.size(); i++) {
      if(sum + arr[i] <= tar) {
          temp.push_back(arr[i]);
          f(arr, ans, temp, tar, sum + arr[i], i);
          temp.pop_back();
      }
  }
  ```
  


#### Revision
- [Generate Parentheses](https://www.geeksforgeeks.org/problems/generate-all-possible-parentheses/1)
- [Subset Sums-1](https://www.geeksforgeeks.org/problems/subset-sums2234/1)
- [Subset Sums-2](https://www.geeksforgeeks.org/problems/subset-sum-ii/1)
- [Combination Sum](https://www.geeksforgeeks.org/problems/combination-sum-1587115620/0)
- [Combination Sum 2](https://www.geeksforgeeks.org/problems/combination-sum-ii-1664263832/1)
- [Combination Sum 3](https://leetcode.com/problems/combination-sum-iii/submissions/1650581574/)
