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

# Sorting
### [Heap Sort](https://www.programiz.com/dsa/heap-sort):
* Time Complexity: BuildMaxHeap (nlogn) + Heapify (nlogn) = nlogn (all cases)
* Space Complexity: O(1)
* Applications: systems concerned with security and embedded system such as Linux Kernel uses Heap Sort because of the O(n log n) upper bound on Heapsort's running time and constant O(1) upper bound on its auxiliary storage. Finding K'th largest / smallest number, priority queues.

### [Counting Sort](https://www.programiz.com/dsa/counting-sort)
* Time Complexity: O(n+k) where k = max element. (all cases)
* Space Complexity: O(k) `// gotta create an array of length k=max with potentially useless spots`
* Counting sort is used when: 
  1. the are smaller integers of multiple counts.
  2. linear complexity is the need.

### [Bucket Sort](https://www.programiz.com/dsa/bucket-sort)
* Time Complexity:
  1. Worst Case: When all elements are placed in the same bucket. Dependent on sorting algo applied on buckets. For insertion sort, o(N<sup>2</sup>)
  2. Avg Case: Linear time. It holds true until the sum of the squares of the bucket sizes is linear in the total number of elements.
  3. Best Case: O(n+k). O(n) is the complexity for making the buckets and O(k) is the complexity for sorting the elements of the bucket using algorithm having linear time complexity at best case.
* Space Complexity: O(n+k), O(nk)
* Bucket sort is used when:
  1. input is uniformly distributed over a range.
  2. there are floating point values
  
### Quick Sort
* TC: Worst N2, Avg & best Nlogn
* Space Complexity: Recursion Stack
* Performs well on arrays. No O(N) extra memory usage required (in-place). Often fast. 

### Selection Sort
* Time Complexity: O(N2) all cases.
* Space Complexity: O(1)
* For N times, select min element and put it in the front of the list. 

### Bubble Sort: 
* Time Complexity: O(N2) worst and average, O(N) best case.
* Space: O(1).
```
for i from 0 to n
  for j from 0 to n-1-i:
    if arr[j] > arr[j+1] swap;
return arr;
```

### Insertion Sort:
* TC: N2 avg & worse, N best
* Space: 1
```
for i from 0 to n:
  put the curr element into correct place among the elements on the right.
```

# JavaScript
* [DS in JS](https://adrianmejia.com/data-structures-time-complexity-for-beginners-arrays-hashmaps-linked-lists-stacks-queues-tutorial/)
* `shift()`: "dequeue" an array
* Sort by ascending numeric order: `arr.sort((a,b) => a-b);` `// The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values.`
* Format number: `(3.2561161).toFixed(2) // 3.25`
* Swap: `[a,b] = [b,a]`
* Increment including undefined: `hash[word] = hash[word]+1||1;`
* Mapping `['a', 'b', ..., 'z']` to `[0, 1, ..., 26]`: `let i = char.charCodeAt() - 97`
* Objects cannot be used as Object keys, they'll be converted to the string `object Object` as the key instead. Use `Map` or `WeakMap` to use Objects as keys.
* `Map` vs `WeakMap`:
  * WeakMap only accepts Objects as keys whereas maps accept any value
  * WeakMap keeps weak references to the objects which allows the garbage collector to clear objects when unreferenced. In relation to this, WeakMap is not enumarable, i.e you can't get a list of its keys.
* Create n by m matrix: `let usedCells = new Array(n).fill().map(() => new Array(m).fill(false));`
