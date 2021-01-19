## Insertion Sort

### Prompt

Write a function that takes in an array of integers and returns a sorted version of that array. Use the Insertion Sort algorithm to sort the array.

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
- Create an outer loop, keeping track of the current index `i`, that will run from `0` through `array.length`.
- Create an inner loop that will run in reverse compared to the outer loop + if `array[current] < array[prev]`, aka needs a swap. So whenever the outer loop index `i` increases, we'll run the inner loop from `j = i` until `j = 0`. This is so we can sort all the subarray from `0 ~ i` for each new `i`.
- Inside the inner loop, swap the `array[j]` with `array[j - 1]` because they're out of order.

__Complexity:__
- Time = O(n^2): We'll run an outer loop through the `n` elements + an inner loop that goes back swapping all the elements out of order.
- Space = O(1): We'll sort the array inplace so we won't need any extra space.

__Code:__

```js
function insertionSort(array) {
  for(let i = 0; i < array.length; i++) {
    for(let j = i; j > 0 && array[j] < array[j - 1]; j--) 
      [array[j], array[j - 1]] = [array[j - 1], array[j]];
  }
  
  return array;
}
```