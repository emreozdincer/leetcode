# Leetcode
Journey with data structures and algorithms

# General Tips
* It is tempting, but not helpful, to abuse the "run" button. Try Easy ones with a goal to get accepted on the first submission, since this more realistically models a whiteboard situation. It forces you to think of all the use cases yourself.

# Trees
* A binary tree has at most 2 child.

### Traversals: 
* Code Always has recursion(left), recursion(right). Only the print statement changes.
* All have time complexity of O(n) where n = # nodes.

* DFS
  1. Pre-order traversal: root-left-right
  2. In-order traversal: left-root-right
  3. Post-order traversal: left-right-root

  **Recursive pseudocode** (other recursive solutons are similar):
  ```
  preorder(node)
    if node === null then return
    visit (node)
    preorder(node.left)
    preorder(node.right)
  ```
  
  **Iterative solution (preorder)**:
  * Utilizes a stack.
  * Constantly pushes right subtree before left subtree so that left subtree is popped and processed earlier in the next iteration.
  * Time Complexity: O(N)
  * Auxiliary Space: O(h). In each iteration, the stack size is increased by 1 at most, and happens *height of tree* times.
  ```javascript
  var preorderTraversal = function(root) {
      if (!root) return []

      const stack = [root];
      const result = []

      while (stack.length > 0) {
          const popped = stack.pop();
          result.push(popped.val)

          if (popped.right) stack.push(popped.right)
          if (popped.left) stack.push(popped.left)
      }

      return result;
  };
  ```
  
  **Iterative solution (inorder)**:
  * Utilizes a stack.
  * Going left until current node is null, pushes each visited node to the stack.
  * Once arrived at null, pops from the stack and prints the value 
  * Time Complexity: O(N)
  * Auxiliary Space: O(h). In each iteration, the stack size is increased by 1 at most, and happens *height of tree* times.
  ```javascript
    var inorderTraversal = function(root) {
      if (!root) return []

      const result = [];
      const stack = [];
      let curr = root;

      while (curr !== null || stack.length > 0) {
          while (curr !== null) {
              stack.push(curr);
              curr = curr.left;
          }
          curr = stack.pop();
          result.push(curr.val);
          curr = curr.right;
      }

      return result;
    };
  ```

* BFS: [Level-order traversal](https://www.youtube.com/watch?v=86g8jAQug04&t=4s&ab_channel=mycodeschool)
  * Time complexity: O(n)
  * Space complexity: O(1) best, O(n) average/worst
  *
  
# JavaScript
* `shift()`: "dequeue" an array
