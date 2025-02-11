# *11. Check for BST*  

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/check-for-bst/1)  

## **Problem Description**  

Given the root of a binary tree, check whether it is a **Binary Search Tree (BST)** or not.  

### **Definition of BST:**  
- The **left subtree** of a node contains only nodes with keys **less than** the node's key.  
- The **right subtree** of a node contains only nodes with keys **greater than** the node's key.  
- **Both** the left and right subtrees must also be binary search trees.  
- **Note:** BSTs **cannot contain duplicate nodes**.  



## **Examples**  

### **Example 1:**  

#### **Input:**  

`root = [2, 1, 3, N, N, N, 5]`

<img src="https://github.com/user-attachments/assets/c5eba8ff-c2eb-4000-82d6-1358f3548d87" width="30%">



#### **Output:**  
```
true
```

#### **Explanation:**  
- The left subtree of every node contains smaller keys and right subtree of every node contains greater keys. 
Hence, **it is a BST**.  



### **Example 2:**  

#### **Input:**  

`root = [2, N, 7, N, 6, N, 9] `

<img src="https://github.com/user-attachments/assets/f45825cc-46bf-421c-825e-f0522f68a7f3" width="30%">


#### **Output:**  
```
false
```

#### **Explanation:**  
- Since the node to the right of node with key `7` has lesser key value,  
Hence, **it is not a BST**.  



### **Example 3:**  

#### **Input:**  

`root = [10, 5, 20, N, N, 9, 25]`

<img src="https://github.com/user-attachments/assets/cc8b90e4-c498-4448-957d-617f59a1d219" width="30%">


#### **Output:**  
```
false
```

#### **Explanation:**  
- The node with key `9` present in the right subtree has lesser key value than root node.  
Hence, **it is not a BST**.  



## **Constraints:**  
- 1 ≤ Number of nodes ≤ $10^5$  
- 1 ≤ node->data ≤ $10^9$  



## **My Approach**  

### ✅ **Min–Max Recursion (Top-Down Approach)**  

1. **Base Case:**  
   - If the current node is `NULL`, return `true` (an empty tree is a valid BST).  

2. **Check Current Node:**  
   - The current node’s value should be **greater than the `min` value** and **less than the `max` value**.  

3. **Recursive Calls:**  
   - Recursively check the left subtree with the updated range `[min, node->data]`.  
   - Recursively check the right subtree with the updated range `[node->data, max]`.  

4. **Return Result:**  
   - The tree is a BST only if **both left and right subtrees** are BSTs.  



## **Time and Auxiliary Space Complexity**  

- **Expected Time Complexity:** `O(N)` We visit each node **exactly once**, performing constant-time operations at each step.  
- **Expected Auxiliary Space Complexity:** `O(H)` Due to the recursion stack, where `H` is the **height of the tree**. In the worst case (skewed tree), `H = N`. In the best case (balanced tree), `H = log N`.  



## Code (C++)

```cpp
class Solution {
public:
    bool isBST(Node* root, int min = INT_MIN, int max = INT_MAX) {
        return !root || (root->data > min && root->data < max &&
                         isBST(root->left, min, root->data) &&
                         isBST(root->right, root->data, max));
    }
};
``` 



<details>
  <summary><h2 align="center">🌲 Alternative Approaches</h2></summary>

## **2️⃣ Inorder Traversal (Recursive)**  

- Perform an **inorder traversal** to produce a list of values.  
- A BST’s inorder traversal should result in a **strictly increasing** sequence.  
- If the sequence is not increasing, the tree is **not a BST**.  

```cpp
class Solution {
    void inorder(Node* root, vector<int>& vals) {
        if (!root) return;
        inorder(root->left, vals);
        vals.push_back(root->data);
        inorder(root->right, vals);
    }
public:
    bool isBST(Node* root) {
        vector<int> vals;
        inorder(root, vals);
        for (int i = 1; i < vals.size(); i++) {
            if (vals[i] <= vals[i-1]) return false;
        }
        return true;
    }
};
```



## **3️⃣ Iterative Inorder Traversal (Using Stack)**  

- Instead of recursion, use a **stack** to simulate inorder traversal.  
- Compare each node’s value with the previous node’s value to check for the BST property.  

```cpp
class Solution {
public:
    bool isBST(Node* root) {
        stack<Node*> st;
        Node* prev = nullptr;
        while (root || !st.empty()) {
            while (root) {
                st.push(root);
                root = root->left;
            }
            root = st.top();
            st.pop();
            if (prev && root->data <= prev->data) return false;
            prev = root;
            root = root->right;
        }
        return true;
    }
};
```



## 📊 **Comparison of Approaches**  

| **Approaches**                        | ⏱️ **Time Complexity** | 🗂️ **Space Complexity** | ⚡ **Method**         | ✅ **Pros**                                  | ⚠️ **Cons**                           |
|-------------------------------------|------------------------|-------------------------|----------------------|---------------------------------------------|--------------------------------------|
| **1️⃣ Min–Max Recursion**             | 🟢 **O(N)**              | 🟡 **O(H)**               | Recursive (Min–Max)   | Fastest; no extra storage                   | Recursive depth may cause stack overflow |
| **2️⃣ Inorder Traversal (Recursive)** | 🟢 **O(N)**              | 🟡 **O(N)**               | Recursive Inorder     | Simple implementation; easy to understand  | Requires extra space for storing nodes   |
| **3️⃣ Iterative Inorder Traversal**   | 🟢 **O(N)**              | 🟡 **O(H)**               | Stack-based DFS       | Avoids recursion stack overflow            | Code complexity is slightly higher      |


## 💡 **Best Choice?**  

- **For Balanced Trees / Small Depth:**  
  ✅ **Approach 1 (Min–Max Recursion)** is the fastest and most efficient.  

- **For Deep or Skewed Trees (Risk of Stack Overflow):**  
  ✅ **Approach 3 (Iterative Inorder Traversal)** handles deep recursion better.  

- **For Simple Understanding & Learning:**  
  ✅ **Approach 2 (Inorder Traversal Recursive)** is the most intuitive to grasp.  

</details>



## Code (Java)

```java
class Solution {
    boolean isBST(Node root) {
        return isBST(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }

    boolean isBST(Node node, int min, int max) {
        return node == null || (node.data > min && node.data < max &&
                isBST(node.left, min, node.data) &&
                isBST(node.right, node.data, max));
    }
}
```



## Code (Python)

```python
class Solution:
    def isBST(self, root, min_val=float('-inf'), max_val=float('inf')):
        return not root or (min_val < root.data < max_val and
                            self.isBST(root.left, min_val, root.data) and
                            self.isBST(root.right, root.data, max_val))
```


