## Nth Fibonacci

### Prompt

The Fibonacci sequence is defined as follows: the first number of the sequence is `0`, the second number is `1`, and the nth number is the sum of the (n - 1)th and (n - 2)th numbers. Write a function that takes in an integer `n` and returns the nth Fibonacci number.
  

**Input**
```js
n = 6
```

**Output**
```js
5 // 0, 1, 1, 2, 3, 5
```

### Solution #1 - Recursively

__Walkthrough:__
- This is an improvement of the naive recursive solution: `return fib(n - 1) + fib(n - 2)`;
- Create a hash table to memoize all the computed fib numbers, to avoid duplicate computations;
- Initialize this hash table(`memo`) with the first two fib numbers: `{ 1: 0, 2: 1 }`;
- In the recursive function, the base case is: if the `n` is in the `memo` hash table, then return the `memo[n]`(we already computed the fib for this number, just return it);
- If we didn't store the `fib(n)`, then compute it and store in the `memo[n] = fib(n - 1) + fib(n - 2)`
- After computing the nth fib, return the `memo[n]`;

__Complexity:__
- Time = O(n): We'll need to compute the fib for all `n`;
- Space = O(n): There will be at max `n` function calls in our call stack;

__Code:__

```js
function getNthFib(n) {
  const memo = { 1: 0, 2: 1 };
  return fib(n);

  function fib(n) {
    if(n in memo) return memo[n];
		
    memo[n] = fib(n - 1) + fib(n - 2);
    return memo[n];
  }
}
```

### Solution #2 - Iteratively

__Walkthrough:__
- We'll need to keep track the last two fib calculations, and we'll update them whenever we compute a new fib;
- Initialize the `lastTwo` with the first 2 fib numbers(It'll always have length 2);
- Create a loop starting at the index `3`(because we have the first 2 fib);
- In the loop update the `lastTwo`: we'll override the `lastTwo[0]` with the `lastTwo[1]` and the `lastTwo[1]` will be the next fib(`lastTwo[0] + lastTwo[1]`);
- To finish, return the `lastTwo[1]` BUT only if the `n > 1`, else return the `lastTwo[0]`;

__Complexity:__
- Time = O(n): We'll need to compute all the `n` fibs;
- Space = O(1): We'll only need 2 variables to store the `lastTwo` fibs;

__Code:__

```js
let lastTwo = [0, 1];

for(let fibCounter = 3; fibCounter <= n; fibCounter++)
  lastTwo = [lastTwo[1], lastTwo[0] + lastTwo[1]];

return n == 1 ? lastTwo[0] : lastTwo[1];
```