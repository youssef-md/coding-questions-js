## Palindrome Check

Write a function that takes in a non-empty string and that returns a boolean representing whether the string is a palindrome.

A palindrome is defined as a string that's written the same forward and backward. Note that single-character strings are palindromes.

### Prompt

**Input**
```js
string = "abcdcba"
```

**Output**
```js
true // it's written the same forward and backward
```

### Solution

__Walkthrough:__
- Create a pointer to the start and the end of the string: `leftIdx`, `rightIdx`.
- Create a loop that will run until `leftIdx < rightIdx`(we'll be comparing the start with the end until the pointer are equal). This loop have to increment the `leftIdx` and decrement the `rightIdx` at the end of every iteration.
- If the `string[leftIdx] != string[rightIdx]` then the `string` isn't a palindrome, return `false`;
- Outside the loop we can return `true`, the code will only run until here if the loop ended and all the chars checks were a palindrome.

__Complexity:__
- Time = O(n): We'll have to have to do at max `n/2` checks, since `1/2` is a constant then the complexity is `O(n)`.
- Space = O(1): We'll only use a `leftIdx` and `rightIdx`.

__Code:__

```js
function isPalindrome(string) {
  let [leftIdx, rightIdx] = [0, string.length - 1];
  
  for(; leftIdx < rightIdx; leftIdx++, rightIdx--)
    if(string[leftIdx] != string[rightIdx])
      return false;
  
  return true;
}

```