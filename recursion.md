# Recursion

## Tree Problems

### Top-down solutions
* Can be considered as a preorder traversal. 

  `top_down(root, params)`
  ```
  1. return specific value for null node
  2. update the answer if needed                      // answer <-- params
  3. left_ans = top_down(root.left, left_params)      // left_params <-- root.val, params
  4. right_ans = top_down(root.right, right_params)   // right_params <-- root.val, params 
  5. return the answer if needed                      // answer <-- left_ans, right_ans
  ```
  
### Bottom-up solutions
* Can be considered as a postorder traversal. 


  `bottom_up(root)`
  ```
  1. return specific value for null node
  2. left_ans = bottom_up(root.left)          // call function recursively for left child
  3. right_ans = bottom_up(root.right)        // call function recursively for right child
  4. return answers                           // answer <-- left_ans, right_ans, root.val
  ```

**Ex: Maximum Depth Problem**

*Top-down*
`maximum_depth(root, depth)`
1. return if root is null
2. if root is a leaf node:
3. answer = max(answer, depth)         // update the answer if needed
4. maximum_depth(root.left, depth + 1)      // call the function recursively for left child
5. maximum_depth(root.right, depth + 1)     // call the function recursively for right child

*Bottom-up*
`bottom_up(root)`
1. return 0 if root is null                 // return 0 for null node
2. left_depth = maximum_depth(root.left)
3. right_depth = maximum_depth(root.right)
4. return max(left_depth, right_depth) + 1  // return depth of the subtree rooted at root

### Conclusion/Suggestions
Can you determine some parameters to help the node know its answer? 
Can you use these parameters and the value of the node itself to determine what should be the parameters passed to its children?
Then `top-down`.

For a node in a tree, if you know the answer of its children, can you calculate the answer of that node? Then `bottom-up`.

### Questions
1. **Symmetric Tree Check**
  * Looking top-down from the root, left subtree and the right subtree must match structurally and value-wise.
  * Null checks ensure structural match, whereas the main part enforces values recursively.
  * Time complexity: Must check every node: O(n)
  * Space complexity: Proportional to the height. In the worst case if we get a skewed tree like a linked-list, even then the algorithm will fail immediately, so it won't be O(n).
 ```javascript
    var isSymmetric = function(root) {
    if (!root) return true;
    
    checkTrees = (left, right) => {
        if (!left && !right) {
            return true;
        } else if (left !== null && right !== null) {
            return left.val === right.val &&
                checkTrees(left.left, right.right) &&
                checkTrees(left.right, right.left)
        } else { // structures dont match
            return false;
        }
    }
    
    return checkTrees(root.left, root.right);
  }; 
  ```
2. **(Root to leaf) [Path Sum](https://leetcode.com/problems/path-sum/)**
  * Time complexity: Must check every node: O(n)
  ```javascript
  var hasPathSum = function(root, sum) {
    var addChild = function (current, child) {
        if (child === null) {
            return false;
        }
        
        const val = current + child.val;
        
        // if leaf, check
        if (!child.left && !child.right){
            return val === sum;
        }
        
        return (addChild (val, child.left) || addChild (val, child.right))
    }
    
    return addChild(0, root);
  };
  ```

## Complexity Analysis

### Time Complexity
* Given a recursion algorithm, its time complexity O(T) is typically the product of the number of recursion invocations (denoted as R) and the time complexity of calculation (denoted as O(s)) that incurs along with each recursion call: O(T)=R∗O(s)
* For recursive functions, it is rarely the case that the number of recursion calls happens to be linear to the size of input. In this case, it is better resort to the execution tree, which is a tree that is used to denote the execution flow of a recursive function in particular. Each node in the tree represents an invocation of the recursive function. Therefore, the total number of nodes in the tree corresponds to the number of recursion calls during the execution.
* Memoization helps

### Space Complexity
* There are mainly two parts of the space consumption that one should bear in mind when calculating the space complexity of a recursive algorithm: recursion related and non-recursion related space.
* **The recursion related space** refers to the memory cost that is incurred directly by the recursion, i.e. the stack to keep track of recursive function calls (each function call keeps 1) the returning address of the function call 2) parameters passed into the function 3) local variables within the function). The function calls stack up (except from *tail recursion*) and might lead to stack overflow.
* **the non-recursion related space** refers to the memory space that is not directly related to recursion, which typically includes the space (normally in heap) that is allocated for the global variables.

### Tail Recursion
* Recursive part is at the end of the function, so the call stack can be optimized to not grow in certain langugages, preventing stack overflow.
