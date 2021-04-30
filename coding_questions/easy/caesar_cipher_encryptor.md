## Caesar Cipher Encryptor

### Prompt

Given a non-empty string of lowercase letters and a non-negative integer representing a key, write a function that returns a new string obtained by shifting every letter in the input string by k positions in the alphabet, where k is the key.

Note that letters should "wrap" around the alphabet; in other words, the letter `z` shifted by one returns the letter `a`.

**Input**
```js
string = "xyz"
key = 2
```

**Output**
```js
"zab"
```

### Solution

__Walkthrough:__
- Create an array that we'll use to mount the new string.
- Create a string with the entire alphabet.
- Create a loop in the input `string` and for each `letter` we'll do:
- - Find the shifted index = current index in the alphabet + the shift.
- - Find the shifted letter = alphabet at `shiftedIndex % 26`(We have to go back when the index > 26).
- - Push this shifted letter in the new string array.
- After running this loop we'll have an array with all shifted letter, so we have to only return the join.

__Complexity:__
- Time = O(n): We need to loop the string only once.
- Space = O(n): We need to store an array of chars for the new shifted string.

__Code:__

```js
function caesarCipherEncryptor(string, shift) {
  const shiftedString = [];
  const alphabet = 'abcdefghijklmnopqrstuvwxyz';

  for(const letter of string) {
    const shiftedIndex = alphabet.indexOf(letter) + shift;
    const shiftedLetter = alphabet[shiftedIndex % 26];
    shiftedString.push(shiftedLetter);
  }
  
  return shiftedString.join('');
}
```