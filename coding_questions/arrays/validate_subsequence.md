
### Prompt

Given two non-empty arrays of integers, write a function that determines whether the second array is a subsequence of the first one.

A subsequence of an array is a set of numbers that aren't necessarily adjacent in the array but that are in the same order as they appear in the array. For instance, the numbers [1, 3, 4] form a subsequence of the array [1, 2, 3, 4], and so do the numbers [2, 4]. Note that a single number in an array and the array itself are both valid subsequences of the array.
  


**Input**
```js
array = [5, 1, 22, 25, 6, -1, 8, 10]
sequence = [1, 6, -1, 10]
```

**Output**
```js
true
```

### Solution

__Walkthrough:__
- Create an index to keep track of the `sequence` array;
- Create a loop with an index that will track the `array`, this loop will run until this `arrayIdx` is smaller than the `array`'s length AND the `sequenceIdx` is smaller than the `sequence`'s length;
- If the `sequence[sequenceIdx]` has the same value of `array[arrayIdx]`, then we found a number that is in the `array`, so increment `sequenceIdx` to keep checking the `sequence` array;
- The code for the loop is done, it'll break if we run the entire `array`, if we run the entire `sequence`, or both;
- Now we have to check if the `sequenceIdx == sequence.length`, if so, then we found in the `array` all the numbers that were in the `sequence`;

__Complexity:__
- Time = O(n): We'll possibly run the entire `array` or `sequence`(wich can be a copy of the `array`);
- Space = O(1): We are using just 2 variables: `sequenceIdx` and `arrayIdx`, this won't grow in consequence of n;

__Code:__

```js
function isValidSubsequence(array, sequence) {
  let sequenceIdx = 0;
  
  for(let arrayIdx = 0; arrayIdx < array.length && sequenceIdx < sequence.length; arrayIdx++) {
    if(sequence[sequenceIdx] == array[arrayIdx])
      sequenceIdx++;      
  }

  return sequenceIdx == sequence.length;
}
```