## First Non-Repeating Character

### Prompt

**Input**
Write a function that takes in a string of lowercase English-alphabet letters and returns the index of the string's first non-repeating character.

The first non-repeating character is the first character in a string that occurs only once.

If the input string doesn't have any non-repeating characters, your function should return `-1`.

```js
string = "abcdcaf"
```

**Output**

```js
1 // The first non-repeating character is "b" and is found at index 1.
```

### Solution

__Walkthrough:__
- We'll use a hash map to keep track of each char count.
- Create a loop through the string to populate this `char_count` with its count.
- After the counting loop, create another loop through the string to find the first non-repeating char. Therefore the first `char_count[string[i]]` that is equal to `1`, then return the index `i`.


**Complexity:**

- Time = O(n): We'll run one loop to populate the `char_count` and outside it we'll run another loop to find the first non-repeating char.
- Space = O(1): Since the max numbers of char count in the hash map is 26 letters. Therefore is a constant.

**Code:**

```js
function firstNonRepeatingCharacter(string) {
  const char_count = {};

  for (char of string)
    char_count[char] = char_count[char] + 1 || 1;

  for (let i = 0; i < string.length; i++)
    if (char_count[string[i]] == 1) return i;

  return -1;
}
```
