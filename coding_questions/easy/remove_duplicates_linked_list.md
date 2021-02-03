## Remove Duplicates from Linked List

### Prompt

You're given the head of a Singly Linked List whose nodes are in sorted order with respect to their values. Write a function that returns a modified version of the Linked List that doesn't contain any nodes with duplicate values. The Linked List should be modified in place (i.e., you shouldn't create a brand new list), and the modified Linked List should still have its nodes sorted with respect to their values.

Each `LinkedList` node has an integer `value` as well as a `next` node pointing to the next node in the list or to `null` if it's the tail of the list.

```js
class LinkedList {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

**Input**
```js
linkedList = 1 -> 1 -> 3 -> 4 -> 4 -> 4 -> 5 -> 6 -> 6 
```

**Output**
```js
1 -> 3 -> 4 -> 5 -> 6 
```

### Solution

__Walkthrough:__
- Create a variable to store the `currentNode`, at first it'll store the head node, `linkedList`.
- Create a loop while `currentNode != null`, aka we aren't at the end.
- Create a variable to store the next distinct node, `nextDistinctNode`.
- Create a loop that will update the `nextDistinctNode` if its `nextDistinctNode.value == currentNode.value`(there is a sequence of duplicates `1 -> 1 -> 1`).
- When exiting the loop above we'll have a true `nextDistinctNode` that its `nextDistinctNode.value != currentNode.value`, so we can "remove" the possible duplicates by updating the pointers:
- - `currentNode.next = nextDistinctNode`, both nodes has distinct values(duplicates were removed).
- - `currentNode = nextDistinctNode`, we are iterating the linked list.

__Complexity:__
- Time = O(n): We'll traverse all the nodes only once.
- Space = O(1): We'll remove the duplicates inplace(updating the pointers `next`).

__Code:__

```js
function removeDuplicatesFromLinkedList(linkedList) {
  let currentNode = linkedList;
  
  while(currentNode != null) {
    let nextDistinctNode = currentNode.next;
    
    while(nextDistinctNode != null && nextDistinctNode.value == currentNode.value)
      nextDistinctNode = nextDistinctNode.next;

    currentNode.next = nextDistinctNode;
    currentNode = nextDistinctNode;
  }

  return linkedList;
}
```