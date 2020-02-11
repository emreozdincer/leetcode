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

  Pseudocode:
  ```
  preorder(node)
    if node === null then return
    visit (node)
    preorder(node.left)
    preorder(node.right)
  ```

* BFS: [Level-order traversal](https://www.youtube.com/watch?v=86g8jAQug04&t=4s&ab_channel=mycodeschool)
  * Time complexity: O(n)
  * Space complexity: O(1) best, O(n) average/worst
  
# JavaScript
* `shift()`: "dequeue" an array
