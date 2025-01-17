# *15. Peak Element*



## **Problem Description**

You are given an array `arr[]` where no two adjacent elements are the same. A **peak element** is defined as an element that is strictly greater than its neighbors. Return the index of any peak element.

**Note:**  
- If the array contains multiple peak elements, you can return the index of any one of them.  
- Assume the element before the first element and the element after the last element are negative infinity (`-∞`).



### **Examples**

**Input:**  
`arr = [1, 2, 4, 5, 7, 8, 3]`  
**Output:**  
`true`  
**Explanation:**  
`arr[5] = 8` is a peak element because `arr[4] < arr[5] > arr[6]`.

**Input:**  
`arr = [10, 20, 15, 2, 23, 90, 80]`  
**Output:**  
`true`  
**Explanation:**  
`arr[1] = 20` and `arr[5] = 90` are peak elements because `arr[0] < arr[1] > arr[2]` and `arr[4] < arr[5] > arr[6]`.

**Input:**  
`arr = [1, 2, 3]`  
**Output:**  
`true`  
**Explanation:**  
`arr[2]` is a peak element because it is the last element and greater than `arr[1]`.



### **Constraints**
- $`1 ≤ arr.size() ≤ 10^6`$
- $`-2^31 ≤ arr[i] ≤ 2^31 - 1`$



## **My Approach**

1. **Binary Search**:
   - This problem can be solved efficiently using **Binary Search**.
   - We divide the array into halves and compare the middle element with its neighbor (`mid+1`).
   - If the middle element is greater than its right neighbor, a peak exists in the left half. Otherwise, it exists in the right half.
   - This ensures a logarithmic complexity.

2. **Steps**:
   - Start with `low = 0` and `high = n-1`.
   - Compute `mid = low + (high - low) / 2`.
   - Compare `arr[mid]` with `arr[mid+1]`:
     - If `arr[mid] > arr[mid+1]`, reduce `high` to `mid`.
     - Otherwise, increase `low` to `mid + 1`.
   - Return `low` as the index of the peak element.



## **Time and Auxiliary Space Complexity**

**Expected Time Complexity:** O(log n), as the binary search reduces the search space by half in every iteration.  
**Expected Auxiliary Space Complexity:** O(1), as no additional space is used apart from a few variables.



## **Code**

## Code (C)

```c
int peakElement(int *arr, int n) {
    int lo = 0, hi = n - 1;

    while (lo < hi) {
        int mid = lo + (hi - lo) / 2;

        if (arr[mid] > arr[mid + 1]) {
            hi = mid;  
        } else {
            lo = mid + 1;  
        }
    }

    return lo;  
}
```

## Code (C++)
```cpp
class Solution {
public:
    int peakElement(vector<int> &arr) {
        int n = arr.size();
        int lo = 0, hi = n - 1;

        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (arr[mid] > arr[mid + 1]) {
                hi = mid; 
            } else {
                lo = mid + 1; 
            }
        }
        return lo; 
    }
};
```

## Code (Java)
```java
class Solution {
    public int peakElement(int[] arr) {
        int low = 0, high = arr.length - 1;

        while (low < high) {
            int mid = low + (high - low) / 2;
            if (arr[mid] > arr[mid + 1]) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low; 
    }
}
```

## Code (Python)
```python
class Solution:
    def peakElement(self, arr):
        low, high = 0, len(arr) - 1

        while low < high:
            mid = low + (high - low) // 2
            if arr[mid] > arr[mid + 1]:
                high = mid
            else:
                low = mid + 1
        
        return low  
```



