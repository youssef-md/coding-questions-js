## Minimum Non-Constructible Change

### Prompt

Given an array of positive integers representing the values of coins in your possession write a function that returns the minimum amount of change (the minimum sum of money) that you can NOT create. The given coins can have any positive integer value and aren't necessarily unique (i.e., you can have multiple coins of the same value).

For example, if you're given `coins = [1, 2, 5]`, the minimum amount of change that you can't create is `4`. If you're given no coins, the minimum amount of change that you can't create is `1`.

**Input**
```js
coins = [5, 7, 1, 1, 2, 3, 22]
```

**Output**
```js
20
```

### Solution

__Walkthrough:__
- The greedy decision is to sort the array.
- Create a varible to count until where we can create a change: `canCreateUntil`.
- Loop through the `sortedCoins` and check if `coin > canCreateUntil + 1`:
- - If true: return `canCreateUntil + 1`(we found the min change that we cannot create).
- - If false: Add the coin to our `canCreateUntil` count.
- Outside the loop we have to return the `canCreateUntil + 1`, because we finished the loop and didn't find the min change that we cannot create in beetween, so the min is the next possible value.


__Complexity:__
- Time = O(n.log(n)): This is due to sorting the array.
- Space = O(1): We don't need to store something that grows by a factor of `n`.

__Code:__

```js
function nonConstructibleChange(coins) {
  const sortedCoins = coins.sort((a, b) => a - b);
  let canCreateUntil = 0;

  for(coin of sortedCoins) {
    if(coin > canCreateUntil + 1) 
      return canCreateUntil + 1;

    canCreateUntil += coin;
  }
  
  return canCreateUntil + 1;
}
```