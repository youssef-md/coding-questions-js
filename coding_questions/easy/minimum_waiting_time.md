## Minimum Waiting Time

### Prompt

You're given a non-empty array of positive integers representing the amounts of time that specific queries take to execute. Only one query can be executed at a time, but the queries can be executed in any order.

A query's waiting time is defined as the amount of time that it must wait before its execution starts. In other words, if a query is executed second, then its waiting time is the duration of the first query; if a query is executed third, then its waiting time is the sum of the durations of the first two queries.

Write a function that returns the minimum amount of total waiting time for all of the queries. For example, if you're given the queries of durations `[1, 4, 5]`, the total waiting time if the queries were executed in the order of `[5, 1, 4]` would be `(0) + (5) + (5 + 1) = 11`. The first query of duration `5` would be executed immediately, to its waiting time would be `0`, the second query of duration `1` would have to wait `5` seconds(the duration of the first query) to be executed, and the last query would have to wait the duration of the first two queries before being executed.
  
**Input**
```js
queries = [3, 2, 1, 2, 6]
```

**Output**
```js
17 // 1 + (1 + 2) + (1 + 2 + 2) + (1 + 2 + 2 + 3)
```

### Solution

__Walkthrough:__
- Create a variable to store the `totalWaitingTime`.
- Sort the array in ascending order(this will garantee that no query has to wait the longest to execute).
- For each query compute the `itemsLeft`, wich is the difference between the `queries.length` with `idx + 1`(`+1` because we need to count the element that starts at `0`).
- Add to the `totalWaitingTime` the `itemsLeft * items`, this way we can compute the time that all `itemsLeft` will have to wait for the query `X` to run, after this loop the `totalWaitingTime` will contain the sum for the minimum waiting time of each query to run.

__Complexity:__
- Time = O(n log(n)): This is the fastest way we can sort an array in every case.
- Space = O(1): We'll only need some variables that aren't related to `N`.

__Code:__

```js
function minimumWaitingTime(queries) {
  let totalWaitingTime = 0;
  const sortedQueries = queries.sort((a, b) => a - b);

  sortedQueries.map((item, idx) => {
    const itemsLeft = queries.length - (idx + 1);
    totalWaitingTime += itemsLeft * item;
  });
  
  return totalWaitingTime;
}

```