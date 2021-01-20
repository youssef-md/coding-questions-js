## Selection Sort

### Prompt

Write a function that takes in an array of integers and returns a sorted version of that array. Use the Selection Sort algorithm to sort the array.

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
- Create an outer loop that will keep track of the `currentIdx`, this index will track the last sorted element in the array. This outer loop will run until `array.length - 1` because we don't need to check the last element, it'll already be sorted.
- Create a variable, `smallestIdx`, to keep the index to the smallest element in the array(we'll need it to swap).
- Create an inner loop that will start from `currentIdx + 1`(in the future will swap the smallest element with the `currentIdx`, that's why the `+1`). This loop will run until `array.length`, its job is to find the smallest element in the array, excluding `0 ~ currentIdx`(they are already sorted).
- - If the `array[smallestIdx] > array[i]`, update the `smallestIdx` to be `i`, we found a smaller element so keep its index.
- Outside the loop that will find the index of the smallest element in the array, perform a swap: we'll swap the `array[currentIdx]` with the `array[smallestIdx]`.

__Complexity:__
- Time = O(n^2): We will need to find the smallest element in the array and swap the latest swapped `+ 1`, this will happen `n` times so `n * n = n^2`;
- Space = O(1): No need for extra space, the sorting will happen in-place.

__Code:__

```js
function selectionSort(array) {
  for(let currentIdx = 0; currentIdx < array.length - 1; currentIdx++) {
    let smallestIdx = currentIdx;
    
    for(let i = currentIdx + 1; i < array.length; i++)
      if(array[smallestIdx] > array[i]) smallestIdx = i;
		
    [array[currentIdx], array[smallestIdx]] = [array[smallestIdx], array[currentIdx]];
  }
  return array;
}
```