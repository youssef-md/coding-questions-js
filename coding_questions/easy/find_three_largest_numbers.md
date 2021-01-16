## Find Three Largest Numbers

### Prompt

Write a function that takes in an array of at least three integers and, without sorting the input array, returns a sorted array of the three largest integers in the input array.

The function should return duplicate integers if necessary; for example, it should return `[10, 10, 12]` for an input array of `[10, 5, 9, 10, 12]`.

**Input**
```js
array  = [141, 1, 17, -7, -17, -27, 18, 541, 8, 7, 7]
```

**Output**
```js
[18, 141, 541]
```

### Solution

__Walkthrough:__
- Create the empty array `threeLargest`.
- For each `num` of the `array`, run the `updateLargest` method(clean code xD), passing the `threeLargest` and the current `num`.
- In the `updateLargest`, we'll have to check if the `first`, `second` or `third` is `null` or smaller than the `num`, and call `shiftAndUpdate`(clean code again xD), passing the `threeLargest`, `num` and the index of the element(`first = 0`, `second = 1`, `third = 2`).
- The `shiftAndUpdate` will loop from `0` until the passed `index`(where the `num` is greater than `first`, `second` or `third`).
- - If `i == idx`: we are at the number that we have to update, so the `threeLargest[i] = num`.
- - Else: We can perform a shift, updating the `threeLargest[i]` to be `threeLargest[i + 1]`(this is to maintain a sorted `threeLargest`).

__Complexity:__
- Time = O(n): Since we can't rely on a sorted array, we'll have to traverse it entirely.
- Space = O(1): We'll just do some comparisons and when shifting, at max 3 attributions.

__Code:__

```js
function findThreeLargestNumbers(array) {
  const threeLargest = [null, null, null]

  for(const num of array)
    updateLargest(threeLargest, num);

  return threeLargest;
}

function updateLargest(threeLargest, num) {
  const [first, second, third] = threeLargest;

  if(!third || num > third)
    shiftAndUpdate(threeLargest, num, 2);
  else if(!second || num > second)
    shiftAndUpdate(threeLargest, num, 1);
  else if(!first || num > first)
    shiftAndUpdate(threeLargest, num, 0);
}

function shiftAndUpdate(array, num, idx) {
  for(let i = 0; i <= idx; i++) {
    if(i == idx)
      array[i] = num;
    else
      array[i] = array[i + 1]
  }
}
```