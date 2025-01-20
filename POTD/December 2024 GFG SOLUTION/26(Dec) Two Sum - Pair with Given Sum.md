# *26. Two Sum - Pair with Given Sum*


## Problem Description

Given an array `arr[]` of positive integers and another integer `target`. Determine if there exist two distinct indices such that the sum of their elements equals `target`.

## **Examples:**

Input:
```
arr[] = [1, 4, 45, 6, 10, 8], target = 16
```
Output:
```
true
```
Explanation: `arr[3] + arr[4] = 6 + 10 = 16`.

Input:
```
arr[] = [1, 2, 4, 3, 6], target = 11
```
Output:
```
false
```
Explanation: None of the pairs makes a sum of 11.

### Constraints
- $1 \leq arr.size \leq 10^5$
- $1 \leq arr[i] \leq 10^5$
- $1 \leq target \leq 2 \times 10^5$



## My Approach

#### Hash Set Approach:
1. Use an unordered set (or `HashSet` in Java / `set` in Python) to track elements as they are traversed.
2. For each element in the array, compute the complement (`target - arr[i]`).
3. Check if the complement exists in the set:
   - If it exists, return `true`.
   - Otherwise, add the current element to the set and continue.
4. If no such pair is found, return `false`.

#### Why this approach?
- Using a hash set allows for $O(1)$ average time complexity for insertion and lookup, ensuring optimal performance.

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** $O(n)$, as we traverse the array once and perform $O(1)$ operations for insertion and lookup in the hash set.
- **Expected Auxiliary Space Complexity:** $O(n)$, as we use a hash set to store up to $n$ elements in the worst case.


## Code (C++)

```cpp
class Solution {
  public:
    bool twoSum(vector<int>& arr, int target) {
        unordered_set<int> seen;
        for (int num : arr) {
            if (seen.count(target - num)) return true;
            seen.insert(num);
        }
        return false;
    }
};
```



## Code (Java)

```java
class Solution {
    boolean twoSum(int[] arr, int target) {
        Set<Integer> seen = new HashSet<>();
        for (int num : arr) {
            if (seen.contains(target - num)) return true;
            seen.add(num);
        }
        return false;
    }
}
```



## Code (Python)

```python
class Solution:
    def twoSum(self, arr, target):
        seen = set()
        for num in arr:
            if target - num in seen:
                return True
            seen.add(num)
        return False
```



