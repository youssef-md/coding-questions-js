## Node Depths

### Prompt

The distance between a node in a Binary Tree and the tree's root is called the node's depth.

Write a function that takes in a Binary Tree and returns the sum of its nodes' depths.

Each `BinaryTree` node has an integer `value`, a `left` child node, and a `right` child node. Children nodes can either be a `BinaryTree` nodes themselves or `null`.

```js
class BinaryTree {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}
```

**Input**
```js
tree =    1
       /     \
      2       3
    /   \   /   \
   4     5 6     7
 /   \
8     9
```

**Output**
```js
16
// The depth of the node with value 2 is 1.
// The depth of the node with value 3 is 1.
// The depth of the node with value 4 is 2.
// The depth of the node with value 5 is 2.
// Etc..
```

### Solution

__Walkthrough:__
- Create an optional parameter `depth`, it will help us to store the running depth sum;
- The base is `if(root == null)`(aka we are outside the tree), then `return 0`;
- The recursive call is: `depth` + recursive call to `root.left` with the increased depth + recursive call to `root.right` with the increased depth;

__Complexity:__
- Time = O(n): We need to traverse the entire tree only once.
- Space = O(h): Where `h` is the tree's height, this will be the max function call in our call stack;

__Code:__

```js
function nodeDepths(root, depth = 0) {
  if(root == null) return 0;
  	
  return depth + nodeDepths(root.left, depth + 1) + nodeDepths(root.right, depth + 1);
}
```