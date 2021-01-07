## Depth-first Search

### Prompt

You're given a `Node` class that has a `name` and an array of optional `children` nodes. When put together, nodes form an acyclic tree-like structure.

```js
class Node {
  constructor(name) {
    this.name = name;
    this.children = [];
  }

  addChild(name) {
    this.children.push(new Node(name));
    return this;
  }

  depthFirstSearch(array) {
    // Write your code here
  }
}
```


Implement the `depthFirstSearch` method on the `Node` class, which takes in an empty array, traverses the tree using the Depth-first Search approach(left-to-rigth), stores all of the node's names in the input array, and returns it.


**Input**
```js
graph = A
     /  |  \
    B   C   D
   / \     / \
  E   F   G   H
     / \   \
    I   J   K
```

**Output**
```js
["A", "B", "E", "F", "I", "J", "C", "D", "G", "K", "H"]
```

### Solution

__Walkthrough:__
- Push the current instance name to the `array`;
- Loop through all the child in the current instance `children` array;
- Call the `depthFirstSearch` for each child and pass the `array` with all the names;
- When the loop finishes, return the `array`

__Complexity:__
- Time = O(V + E): Since we want to visit all the nodes(vertices) -> O(V) + Each node has a number E of edges and we'll traverse them recursively. Therefore V + E;

- Space = O(V): This will be the max number of recursive `depthFirstSearch` calls in the call stack for an unbalanced graph.

__Code:__

```js
class Node {
  constructor(name) {
    this.name = name;
    this.children = [];
  }

  addChild(name) {
    this.children.push(new Node(name));
    return this;
  }

  depthFirstSearch(array) {
    array.push(this.name);
    
    for(const child of this.children) 
      child.depthFirstSearch(array)

    return array;
  }
}
```