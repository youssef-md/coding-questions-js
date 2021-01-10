## Binary Search

### Prompt

Write a function that takes in a sorted array of integers as well as a target integer. The function should use the Binary Search algorithm to determine if the target integer is contained in the array and should return its index if it is, otherwise `-1`.

**Input**
```js
array = [0, 1, 21, 33, 45, 45, 61, 71, 72, 73]
target = 33
```

**Output**
```js
3
```

### Solution #1 - Recursively

__Walkthrough:__
- Define the `left` as `0` and `right` as `array.length - 1`;
- The base case is if `left > right`, aka we didn't find the target in the array.
- Compute the `middle` as being the floor of `(left / 2) + (right / 2)`(this prevent an overflow, compared with `(left + right) / 2`;
- Check if the `array` at the `middle` is the target, if true, just return the `middle`(this is the index of the target);
- Else if the `target > array[middle]`, the target is in the higher subarray, so return a recursive call to the `binarySearch` passing the `middle + 1` as the new `left`.
- Else, the `target` is lower than the `array[middle]`, so we have to check the lower subarray, we can do this by returning a recursive call to the `binarySearch` passing the `middle - 1` as the new `right`.

__Complexity:__
- Time = O(log(n)): For each iteration we are eliminating half of the array.
- Space = O(log(n)): We'll need at max log(n) space due to the recursion(new function calls in the call stack).

__Code:__

```js
function binarySearch(array, target, left = 0, right = array.length - 1) {
  if(left > right) return -1;
  
  const middle = Math.floor((left / 2) + (right / 2));
  const potentialMatch = array[middle];
	
  if(target == potentialMatch)
    return middle;
  else if(target > potentialMatch)
    return binarySearch(array, target, middle + 1, right);
  else
    return binarySearch(array, target, left, middle - 1);
}
```

### Solution #2 - Iteratively

__Walkthrough:__
- Define the `left` as `0` and `right` as `array.length - 1`;
- Create a loop that will run while `left <= right` the left and right pointers haven't cross, aka the target may be in the array.
- Compute the `middle` as being the floor of `(left / 2) + (right / 2)`(this prevent an overflow, compared with `(left + right) / 2`;
- Now check if the target is `==`, `<`, or `>` than the `array[middle]`
- - If is equal: just return the `middle`(the index of the target).
- - If is greater than: the `target` may be at the end portion of the array, so update the `left` to be `middle + 1`(ignore the left part of the `array`);
- - If is less than: the `target` may be at the start portion of the array, so update the `right` to be `middle - 1`(ignore the right part of the `array`);

__Complexity:__
- Time = O(log(n)): For each iteration we are eliminating half of the array.
- Space = O(1): We are just computing some variables.

__Code:__

```js
function binarySearch(array, target) {
  let left = 0, right = array.length - 1;
  
  while(left <= right) {
    const middle = Math.floor((left / 2) + (right / 2));
    const potentialMatch = array[middle];
    
    if(target == potentilMatch)
      return middle;
    else if(target > potentialMatch)
      left = middle + 1;
    else
      right = middle - 1;
	}
  return -1;
}
```