
## Find Closest Value in BST

### Prompt

Write a function that takes in a Binary Search Tree (BST) and a target integer value and returns the closest value to that target value contained in the BST.

You can assume that there will only be one closest value.

Each BST node has an integer `value`, a `left` child node, and a `right` child node. A node is said to be a valid BST node if and only if it satisfies the BST property: its `value` is strictly greater than the values of every node to its left; its `value` is less than of equal to the values of every node to its right; and its children nodes are either valid BST nodes themselves or `null`.

The BST is constructed by this class:
```js
class BST {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}
```

**Input**
```js
tree =   10
       /     \
      5      15
    /   \   /   \
   2     5 13   22
 /           \
1            14

target = 12
```

**Output**
```js
13
```

### Solution #1 - Recursively

__Walkthrough:__
- Create a helper function that will be called recursively, this function will receive the tree, the target and the current closest value to its target;
- The base case is if `tree == null` (aka we are outside the leaf), therefore return the `closest` value that we found;
- Now we can check the absolute diff between `target - closest` and `target - tree.value`. If the `|target - closest| > |target - tree.value|` then we found a new `closest` value, so update it;
- After Updating(or not) the `closest` we can perform a recursive search in the BST:
- - `target < tree.value`: Then check only the `tree.left`;
- - `target > tree.value`: Then check only the `tree.right`;
- - `target == tree.value` (aka we found exactly the target in the BST): return the `tree.value`;

__Complexity:__
- Average Time = O(log(n)): We are performing a search in a BST, so we'll cut in half for each iteration;
- Average Space = O(log(n)): We'll need `log(n)` function calls in our call stack, since we are using recursion;
- Worst Time = O(n): In an unbalenced BST, we'll perform a linear search;
- Worst Space = O(n): We'll need `n` function calls in our call stack, since we are using recursion;

__Code:__

```js
function findClosestValueInBstHelper(tree, target, closest) {
  if(tree == null)
    return closest;

  if(Math.abs(target - closest) > Math.abs(target - tree.value))
    closest = tree.value;

  if(target < tree.value)
    return findClosestValueInBstHelper(tree.left, target, closest)
  else if(target > tree.value)
    return findClosestValueInBstHelper(tree.right, target, closest)
  else
    return tree.value
}

function findClosestValueInBst(tree, target) {
  return findClosestValueInBstHelper(tree, target, tree.value);
}
```

### Solution #2 - Iteratively

__Walkthrough:__
- We'll need two varibles for this, `currentNode`: it'll be updated based on our traversy, `closest`: it'll be updated to store the current closest value to the target;
- After initializing the `currentNode` with the first node of the `tree`, create a loop that will run while `currentNode != null`(aka we aren't outside the leaf);
- Compare if: `|target - closest| > |target - currentNode.value|`, if true, update the `closest` to be `currentNode.value` since the current node has a value that is closest to the `target` than the `closest` :D;
- Now perform an iterative search in the BST, updating the `currentNode`;

__Complexity:__
- Average Time = O(log(n)): We are performing a search in a BST, so we'll cut in half for each iteration;
- Average Space = O(1): We are using just two variables, the space need will never grow;
- Worst Time = O(n): In an unbalenced BST, we'll perform a linear search;
- Average Space = O(1): We are using just two variables, the space need will never grow;

__Code:__

```js
function findClosestValueInBst(tree, target) {
  let currentNode = tree;
  let closest = tree.value;

  while(currentNode != null) {
    if(Math.abs(target - closest) > Math.abs(target - currentNode.value))
      closest = currentNode.value;
    if(target < currentNode.value)
      currentNode = currentNode.left;
    else if (target > currentNode.value)
      currentNode = currentNode.right
    else
      break;
  }
	
  return closest;
}
```