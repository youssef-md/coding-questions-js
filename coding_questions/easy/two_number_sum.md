
## Two Number Sum

### Prompt

Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. If any two numbers in the input array sum up to the target sum, the function should return them in an array, in any order. If no two numbers sum up to the target sum, the function should return an empty array.

**Input**
```js
array = [3, 5, -4, 8, 11, -1, 6]
target = 10
```

**Output**
```js
[-1, 11]
```

### Solution

__Walkthrough:__
- Create a hash table(JS object);
- Loop through the array;
- We want to find the `pair` such as `current + pair = target` -> `pair = target - current`;
- Check if the `pair` is stored in the hash table;
- If so, we found two numbers that adds to the target: `current` + `pair`;
- If not, store the `current` in the hash table so when its `pair` appears it'll find it in the hash table;

__Complexity:__
- Time = O(n): We are looping the array only once;
- Space = O(n): We are storing until `n` numbers in the hash table;

__Code:__

```js
function twoNumberSum(array, target) {
  const visited = {};

  for(current of array) {
    const pair = target - current;

    if(visited[pair])
      return [current, pair];
    else
      visited[current] = true;
  }

  return [];
}
```