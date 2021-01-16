## Bubble Sort

### Prompt

Write a function that takes in an array of integers and returns a sorted
version of that array. Use the Bubble Sort algorithm to sort the array.

**Input**
```js
array = [8, 5, 2, 9, 5, 6, 3]
```

**Output**
```js
[2, 3, 5, 5, 6, 8, 9]
```

### Solution

__Walkthrough:__
- Create a flag `isSorted` se we'll know when to stop the outer loop.
- Create the outer loop creating a variable `finalIndexes` to count how many elements are in their final position, so we won't need to run a the swap check on them.
- Set the `isSorted` to `true`, it'll keep being `true` only if none of the elements are swaped, in this case the array will be sorted, therefore break the loop.
- Create the inner loop that will run until `array.length - 1 - finalIndexes`, `array.length - 1` because we'll check the `i` and `i + 1` inside the loop, and `... - finalIndexes` because we don't have to run throught the entire `n` elements when there are `finalIndexes` of elements already in their final positions.
- Check if the current element is greater than the next element, `array[i] > array[i + 1]`.
- - If `true`, swap them and set the `isSorted` to `false`, to keep running the outer loop.

__Complexity:__
- Time = O(n^2): We'll run an external loop while the array isn't sorted + an inner loop to swap the needed elements.
- Space = O(1): We'll sort the array inplace so we won't need any extra space.

__Code:__

```js
function bubbleSort(array) {
  let isSorted = false;

  for(let finalIndexes = 0; !isSorted; finalIndexes++){
    isSorted = true;

    for(let i = 0; i < array.length - 1 - finalIndexes; i++) {
      if(array[i] > array[i + 1]) {
        [array[i], array[i + 1]] = [array[i + 1], array[i]];
        isSorted = false				
      }
    }
  }
  return array;
}
```