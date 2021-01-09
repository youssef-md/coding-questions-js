## Product Sum

### Prompt

Write a function that takes in a "special" array and returns its product sum.

A "special" array is a non-empty array that contains either integers or other "special" arrays. The product sum of a "special" array is the sum of its elements, where "special" arrays inside it are summed themselves and then multiplied by their level of depth.

The depth of a "special" array is how far nested it is. For instance, the depth of `[]` is `1`; the depth of the inner array in `[[]]` is `2`; the depth of the innermost array in `[[[]]]` is `3`.

Therefore, the product sum of `[x, y]` is `x + y`; the product sum of `[x, [y, z]]` is `x + 2 * (y + z)`; the product sum of `[x, [y, [z]]]` is `x + 2 * (y + 3 * z)`.

**Input**
```js
array = [5, 2, [7, -1], 3, [6, [-13, 8], 4]]
```

**Output**
```js
12 // calculated as: 5 + 2 + 2 * (7 - 1) + 3 + 2 * (6 + 3 * (-13 + 8) + 4)
```

### Solution

__Walkthrough:__
- Add an optative parameter `multiplier` initialized with `1`(this will help us in the recursive calls);
- Create a variable to store the `sum`;
- Run a loop for each item;
- If the item is an array, add to the `sum` a function call `productSum(item, multiplier + 1)`(this will return the inner sum mutiplied with the new multiplier based on its depth);
- If the item isn't an array, just sum the item with the `sum`;
- Outside the loop, return the `sum * multiplier`;

__Complexity:__
- Time = O(n): Where `n` is all the numbers of the array and the subarrays;
- Space = O(d): Where `d` is the depth of the subarrays, because for each new array we'll have a new function call in our call stack;

__Code:__

```js
function productSum(array, multiplier = 1) {
  let sum = 0;

  for(const item of array) {
    if(Array.isArray(item))
      sum += productSum(item, multiplier + 1);
    else
      sum += item;
  }

  return sum * multiplier;
}
```