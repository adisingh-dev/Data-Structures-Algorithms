
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
  


#### Revision
- [Combination Sum](https://www.geeksforgeeks.org/problems/combination-sum-1587115620/0)
- [Combination Sum 2](https://www.geeksforgeeks.org/problems/combination-sum-ii-1664263832/1)
- [Generate Parentheses](https://www.geeksforgeeks.org/problems/generate-all-possible-parentheses/1)
