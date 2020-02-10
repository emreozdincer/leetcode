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
