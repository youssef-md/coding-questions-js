## Tandem Bicycle

### Prompt

A tandem bicycle is a bicycle that's operated by two people: person A and person B. Both people pedal the bicycle, but the person that pedals faster dictates the speed of the bicycle. 

You're given two lists of positive integers: one that contains the speeds of riders wearing red shirts and one that contains the speeds of riders wearing blue shirts. Each rider is represented by a single positive integer, which is the speed that they pedal a tandem bicycle at. Both lists have the same length, meaning that there are as many red-shirt riders as there are blue-shirt riders. Your goal is to pair every rider wearing a red shirt with a rider wearing a blue shirt to operate a tandem bicycle.

Write a function that returns the maximum possible total speed or the minimum possible total speed of all of the tandem bicycles being ridden based on an input parameter, `fastest`. If `fastest = true`, your function should return the maximum possible total speed; otherwise it should return the minimum total speed.

**Input**
```js
redShirtSpeeds = [5, 5, 3, 9, 2]
blueShirtSpeeds = [3, 6, 7, 2, 1]
fastest = true
```

**Output**
```js
32
```

### Solution

__Walkthrough:__
- The greedy approach is to sort the arrays, if `fastest = true` sort both arrays is ascending order; otherwise, sort one in ascending and another in descending orders. This will enable us to match the `max, min` value in the first array combination, and `max, max` is the second.
- Create an accumulator that will store the max speed count.
- Loop and create two indexes: `i` and `j`:
- - `i` will go from `0` until the end.
- - `j` will fo from the end until `0`.
- Sum the result of `Math.max(sortedReds[i], sortedBlues[j])` with the `acc`
- - This `max` result above will be the pair: `max, min` values if both arrays are in ascending orders, this way we'll get the fastest speed sum. But if `fastest = false` it'll pair: `max, max` values, so we can elliminate the `max` values for each iteration, resulting in the slowest speed sum.

__Complexity:__
- Time = O(n.log(n)): We'll need to sort the arrays.
- Space = O(1): The sort in inplace and we'll only do some checks.

__Code:__

```js
function tandemBicycle(redShirtSpeeds, blueShirtSpeeds, fastest) {
  
  const sortedReds = redShirtSpeeds.sort((a, b) => a - b);
  const sortedBlues = blueShirtSpeeds.sort((a, b) => fastest ? a - b : b - a);
  let acc = 0;
  
  for(let i = 0, j = sortedReds.length - 1; j >= 0; i++, j--)
    acc += Math.max(sortedReds[i], sortedBlues[j]);
    
  return acc;
}
```