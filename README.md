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
  
  To serialize a node (to identify it in a HashMap etc.):
  ```javascript
  const serialize = node => {
    if (!node) return '#'

    let str = node.val + ',' + serialize(node.left) + ',' + serialize(node.right);

    return str;
  }
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
  
  **MEDIUM/HARD - iterative solution for [inorder](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)**
  
  **HARD - iterative solution for [postorder](https://www.geeksforgeeks.org/iterative-postorder-traversal/)**

* BFS: [Level-order traversal](https://www.youtube.com/watch?v=86g8jAQug04&t=4s&ab_channel=mycodeschool)
  * Time complexity: O(n)
  * Space complexity: O(1) best, O(n) average/worst
  
# Queues and Stacks
* Circular queue (aka *Ring Buffer*) implementation is smart in that it enables you to use allocated space continously, utilizing 'head' and 'tail' pointers and moving them around.

### Questions
#### [Number of Islands](https://leetcode.com/problems/number-of-islands/)
* Can utilize BFS with a queue.
* Start from top-left, 2D loop.
* If the node is not visited & has land, mark as visited, increment the land counter, and apply BFS to find all neighboring lands and mark them as visited as well.
* Time complexity : O(M×N)

#### [Stack with min(stack) operation in O(1)](https://www.youtube.com/watch?v=8Ub73n4ySYk&ab_channel=IDeserve)
* Utilize two stacks, first being usual and the second to keep track of the minimum values.
* If a newly pushed element is less than the current minimum (which is indicated from top of the 2nd stack), then push it to second stack as well.
* Time Complexity: Push, pop, getMin O(1)
* Space Complexity: Worst Case O(N)

#### [Daily Temperatures](https://www.youtube.com/watch?v=WGm4Kj3lhRI&ab_channel=AlexanderLe)
* Start iterating from the end. Use a stack to intelligently track the increasing degrees. 
* Time Complexity: O(N), where N is the length of T and W is the number of allowed values for T[i]. Each index gets pushed and popped at most once from the stack.
* Space Complexity: O(W). The size of the stack is bounded as it represents strictly increasing temperatures.

# JavaScript
* [DS in JS](https://adrianmejia.com/data-structures-time-complexity-for-beginners-arrays-hashmaps-linked-lists-stacks-queues-tutorial/)
* `shift()`: "dequeue" an array
* Sort by ascending numeric order: `arr.sort((a,b) => a-b);` `// The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values.`
* Format number: `(3.2561161).toFixed(2) // 3.25`
* Swap: `[a,b] = [b,a]`
* Increment including undefined: `x['a'] = (x['a'] || 0) + 1`
* Mapping `['a', 'b', ..., 'z']` to `[0, 1, ..., 26]`: `let i = char.charCodeAt() - 97`
