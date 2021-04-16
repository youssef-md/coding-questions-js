## Run-Length Encoding

### Prompt

Write a function that takes in a non-empty string and returns its run-length encoding.

From Wikipedia, "run-length encoding is a form of lossless data compression in which runs of data are stored as a single data value and count, rather than as the original run." For this problem, a run of data is any sequence of consecutive, identical characters. So the run `"AAA"` would be run-length as `"3A"`.

To make things more complicated, however, the input string can contain all sorts of special characters, including numbers. And since encoded data must be decodable, this means that we can't naively run-length-encode long runs. For example, the run `"AAAAAAAAAAAA"`(12 `A`s), can't naively be encoded as `"12A"`, since this string can be decoded as either `"AAAAAAAAAAAA"` or `"1AA"`. Thus long runs( > 10 chars) should be encoded in a split fashion: `"9A3A"`.

**Input**
```js
string = "AAAAAAAAAAAAABBCCCCDD"
```

**Output**
```js
"9A4A2B4C2D"
```

### Solution

__Walkthrough:__
- We have to keep a count of how many times we've seen a char together, and reset this count when it's `== 9`.
- Create a list to store each new pair of `char + count`.
- Create a counter variable starting from `1`(the prompt says there won't the string of size `0` and the loop will only run when > 1).
- Start a loop from `i = 1`(we'll get the prev char) until `i < string.length`.
- Inside the loop get the current: `curr` and previous: `prev`, characters of the string.
- Check for the end of an encoding: `curr != prev` OR `count == 9`.
- - If true, push to the `list` the pair: `count prev`.(It's `prev` we are counting the `prev` ) And reset the count to `0`.
- At the end of the loop increment the count.
- After the loop we'll have a list of pairs `count prev` of each char EXCEPT the last one. Since we're pushing the `prev`, the last item would the the `curr` and it wouldn't be added to the list, so we just have to add it. This will handle if the input `string` has only one char too.

__Complexity:__
- Time = O(n): We'll traversing the `string` only once.
- Space = O(n): We'll keeping track of a list that can have size `n`.

__Code:__

```js
function runLengthEncoding(string) {
  const list = [];
  let count = 1;

  for(let i = 1; i < string.length; i++) {
    const [curr, prev] = [string[i], string[i - 1]];

    if(curr != prev || count == 9) {
      list.push(`${count}${prev}`);
      count = 0;
    }
    
    count++;
  }

  list.push(`${count}${string[string.length - 1]}`);
  
  return list.join('');
}
```