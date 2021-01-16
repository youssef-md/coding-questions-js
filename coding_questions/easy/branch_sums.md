## Branch Sums

### Prompt

Write a function that takes in a Binary Tree and returns a list of its branch sums ordered from leftmost branch sum to rightmost branch sum.

A branch sum is the sum of all values in a Binary Tree branch. A Binary Tree branch is a path of nodes in a tree that starts at the root node and ends at any leaf node.

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
     /   \    /  \
    4     5  6    7
  /   \  /
 8    9 10
```

**Output**
```js
[15, 16, 18, 10, 11]
// 15 == 1 + 2 + 4 + 8
// 16 == 1 + 2 + 4 + 9
// 18 == 1 + 2 + 5 + 10
// 10 == 1 + 3 + 6
// 11 == 1 + 3 + 7
```

### Solution

__Walkthrough:__
- Create an array to store the sums of the branches.
- Create a helper method, for recursion, that receives the `node`, a `runningSum`(this will keep track of the current execution sum), and the `sums` array.
- Call a helper method passing all its params.
- In the recursive method, base case 01: check if `!node` then return.
- Sum the `runningSum` with the current `node.value`.
- Base case 02: if we are in a leaf node(`!node.left && !node.right`), push the `newRunningSum` to the `sums` array and return.
- Create two recursive calls, passing `node.left` and `node.right`.
- The recursion magic will run a DFS(Depth-First-Search) and sum all the branches of the Binary Tree.

__Complexity:__
- Time = O(n): We'll visit all the `N` nodes + some O(1) operations.
- Space = O(n): Since in a Binary Tree each layer is double of the previous and for this problem we have to reach all the leaf nodes, we'll need `N/2` function call. + There can't be more than `N` branches.

__Code:__

```js
function branchSums(root) {
  const sums = [];
  
  calcBranchSums(root, 0, sums);
  
  return sums;
}

function calcBranchSums(node, runningSum, sums) {
  if(!node) return;
  
  const newRunningSum = runningSum + node.value;
  
  if(!node.left && !node.right) {
    sums.push(newRunningSum);
    return;
  }

  calcBranchSums(node.left, newRunningSum, sums);
  calcBranchSums(node.right, newRunningSum, sums);
}
```