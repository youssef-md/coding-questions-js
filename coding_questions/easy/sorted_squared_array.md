## Sorted Squared Array

### Prompt

Write a function that takes in a non-empty array of integers that are sorted in ascending order and returns a new array of the same length with the squares of the original integers also sorted in ascending order.

**Input**
```js
array = [-3, -2, 0, 1, 2, 6, 9];
```

**Output**
```js
[0, 1, 4, 4, 9, 36, 81]
```

### Solution

__Walkthrough:__
- If there weren't negative numbers, this question would be super dumb. The only thing we have to remember is that  `negative * negative = positive`, so we have to check the absolute value to determine who is greater.
- Start by creating a new array with the same input's array size.
- Define some variables that we'll use: `left`(initial left pointer to the start of the array), `right`(initial right pointer to the end of the array) and `greaterAbs`(the variable that we'll use to store the greater value for each iteration).
- Create a loop defining the `idx`(this is our pointer were in our new array `squared` we can insert a number). This loop will run until `idx >= 0`, aka we have no more space in the array.
- Now let's check the absolute value of the `array[left]` and `array[right]`, the greater value is the one we want, so we can insert in the `squared` array from the largest number to the smallest.
- - If the `Math.abs(array[left]) > Math.abs(array[right]`: The left pointer points to the greater value, so store it and move the left pointer: `left++`.
- - Else, aka `Math.abs(array[left]) <= Math.abs(array[right]`: The right pointer points to the greater value, so store it and move the right pointer: `right--`.
- After this check, we know wich is the greater value from this iteration, so we can insert and the current available end of the `sorted` array.

__Complexity:__
- Time = O(n): We'll traverse the input array only once.
- Space = O(n): We'll create a new array with the same input's array size.

__Code:__

```js
function sortedSquaredArray(array) {
  const squared = new Array(array.length).fill(0);
  let [left, right, greaterAbs] = [0, array.length - 1, 0];

  for(let idx = array.length - 1; idx >= 0; idx--) {
    if(Math.abs(array[left]) > Math.abs(array[right])) {
      greaterAbs = array[left];
      left++;
    } else {
      greaterAbs = array[right];
      right--;
    }
    squared[idx] = greaterAbs * greaterAbs;
  }

  return squared;
}
```