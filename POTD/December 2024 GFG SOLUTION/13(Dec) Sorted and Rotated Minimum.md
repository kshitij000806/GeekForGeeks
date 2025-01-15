# *13. Sorted and Rotated Minimum*  



## Problem Description

You are given a sorted array `arr[]` which has been rotated at an unknown pivot. The array may contain duplicate elements. Your task is to find the **minimum element** in the array.

### Examples:

**Input:**  
`arr[] = [5, 6, 1, 2, 3, 4]`  
**Output:**  
`1`  
**Explanation:**  
The minimum element is `1`.

**Input:**  
`arr[] = [3, 2, 2, 2]`  
**Output:**  
`2`  
**Explanation:**  
The minimum element is `2`.

**Input:**  
`arr[] = [4, 4, 4]`  
**Output:**  
`4`  
**Explanation:**  
The minimum element is `4`.

### Constraints:
- `1 ≤ arr.size() ≤ 10^6`
- `1 ≤ arr[i] ≤ 10^9`


## My Approach

1. **Binary Search in a Rotated Array:**  
   - To find the minimum element in a rotated sorted array, we leverage **binary search** to reduce the search space efficiently.
   - Use two pointers, `lo` and `hi`, to represent the current range. Compare the middle element with the last element to determine the rotation point.

2. **Handling Duplicates:**  
   - When duplicates are present, special handling is required to ensure correctness. In such cases, we adjust the `hi` pointer if `arr[mid]` equals `arr[hi]`.

3. **Steps:**  
   - Initialize two pointers, `lo` and `hi`, to the start and end of the array.  
   - If `arr[lo] < arr[hi]`, the array is not rotated, and `arr[lo]` is the minimum.  
   - Compute the middle index `mid`.  
   - Compare `arr[mid]` with `arr[hi]`:  
     - If `arr[mid] > arr[hi]`, the minimum is in the right half (`lo = mid + 1`).  
     - If `arr[mid] < arr[hi]`, the minimum is in the left half (`hi = mid`).  
     - If `arr[mid] == arr[hi]`, decrement `hi` to handle duplicates.  
   - Return `arr[lo]` as the minimum element.


## Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(log n), as we reduce the search space by half in each iteration. In the case of duplicates, the complexity degrades to O(n).  
- **Expected Auxiliary Space Complexity:** O(1), as we use only a constant amount of additional space.


## Code (C)

```c
int findMin(int* arr, int n) {
    int lo = 0, hi = n - 1;
    while (lo < hi) {
        if (arr[lo] < arr[hi])
            return arr[lo];
        int mid = lo + ((hi - lo) >> 1);
        if (arr[mid] > arr[hi])
            lo = mid + 1;
        else
            hi = mid;
    }
    return arr[lo];
}
```


## Code (Cpp)

```cpp
class Solution {
public:
    int findMin(vector<int>& arr) {
        int lo = 0, hi = arr.size() - 1;
        while (lo < hi) {
            if (arr[lo] < arr[hi])
                return arr[lo];
            int mid = lo + ((hi - lo) >> 1); 
            if (arr[mid] > arr[hi])
                lo = mid + 1;
            else
                hi = mid;
        }

        return arr[lo];
    }
};
```


## Code (Java)

```java
class Solution {
    public int findMin(int[] arr) {
        int lo = 0, hi = arr.length - 1;
        while (lo < hi) {
            if (arr[lo] < arr[hi])
                return arr[lo];
            int mid = lo + ((hi - lo) >> 1);
            if (arr[mid] > arr[hi])
                lo = mid + 1;
            else
                hi = mid;
        }
        return arr[lo];
    }
}
```


## Code (Python)

```python
class Solution:
    def findMin(self, arr):
        lo, hi = 0, len(arr) - 1
        while lo < hi:
            if arr[lo] < arr[hi]:
                return arr[lo]
            mid = lo + ((hi - lo) // 2)
            if arr[mid] > arr[hi]:
                lo = mid + 1
            else:
                hi = mid
        return arr[lo]
```


