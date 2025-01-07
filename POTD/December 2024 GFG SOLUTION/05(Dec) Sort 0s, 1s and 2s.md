# *5. Sort 0s, 1s, and 2s*



## Problem Description

You are given an array `arr[]` containing only 0s, 1s, and 2s. The task is to sort the array in ascending order. The problem must be solved **in-place**, and the space complexity should be constant.

### Examples:

**Input:**  
`arr[] = [0, 1, 2, 0, 1, 2]`  
**Output:**  
`[0, 0, 1, 1, 2, 2]`

**Explanation:**  
The array is sorted into ascending order.

**Input:**  
`arr[] = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1]`  
**Output:**  
`[0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2]`

**Explanation:**  
The array is sorted into ascending order.

### Constraints:
- `1 <= arr.size() <= 10^6`
- `0 <= arr[i] <= 2`



## My Approach

1. **Dutch National Flag Algorithm**:  
   - This problem can be solved using a two-pointer approach, also known as the Dutch National Flag Algorithm.  
   - It divides the array into three sections:  
     - All `0s` will be placed at the beginning.  
     - All `2s` will be placed at the end.  
     - All `1s` will remain in the middle.  
   - By iterating through the array and performing swaps, we can sort the array in a single pass.

2. **Steps:**  
   - Initialize three pointers: `low`, `mid`, and `high`.  
   - Use `low` to track the position of `0s`, `high` to track the position of `2s`, and `mid` to traverse the array.  
   - Swap elements as necessary to place `0s`, `1s`, and `2s` in their respective positions.  
   - Continue until `mid` crosses `high`.



## Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n), as we iterate through the array exactly once, performing constant-time operations during each step.  
- **Expected Auxiliary Space Complexity:** O(1), as we use only three pointers (`low`, `mid`, `high`) and no extra data structures.



## Code (C)

```c
void sort012(int arr[], int n) {
    int low = 0, mid = 0, high = n - 1;

    while (mid <= high) {
        switch (arr[mid]) {
            case 0:
                {
                    int temp = arr[low];
                    arr[low] = arr[mid];
                    arr[mid] = temp;
                }
                low++;
                mid++;
                break;

            case 1:
                mid++;
                break;

            case 2:
                {
                    int temp = arr[high];
                    arr[high] = arr[mid];
                    arr[mid] = temp;
                }
                high--;
                break;
        }
    }
}
```



## Code (Cpp)

```cpp
class Solution {
public:
    void sort012(vector<int>& arr) {
        int low = 0, mid = 0, high = arr.size() - 1;

        while (mid <= high) {
            switch (arr[mid]) {
                case 0:
                    swap(arr[mid++], arr[low++]);
                    break;
                case 1:
                    mid++;
                    break;
                case 2:
                    swap(arr[mid], arr[high--]);
                    break;
            }
        }
    }
};
```



## Code (Java)

```java
class Solution {
    public void sort012(int[] arr) {
        int low = 0, mid = 0, high = arr.length - 1;

        while (mid <= high) {
            switch (arr[mid]) {
                case 0:
                    int temp0 = arr[low];
                    arr[low] = arr[mid];
                    arr[mid] = temp0;
                    low++;
                    mid++;
                    break;

                case 1:
                    mid++;
                    break;

                case 2:
                    int temp2 = arr[high];
                    arr[high] = arr[mid];
                    arr[mid] = temp2;
                    high--;
                    break;
            }
        }
    }
}
```



## Code (Python)

```python
class Solution:
    def sort012(self, arr):
        low, mid, high = 0, 0, len(arr) - 1

        while mid <= high:
            if arr[mid] == 0:
                arr[low], arr[mid] = arr[mid], arr[low]
                low += 1
                mid += 1
            elif arr[mid] == 1:
                mid += 1
            else:
                arr[mid], arr[high] = arr[high], arr[mid]
                high -= 1
```




