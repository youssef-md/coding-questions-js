## Generate Document

### Prompt

You're given a string of available characters and a string representing a
document that you need to generate. Write a function that determines if you
can generate the document using the available characters. If you can generate
the document, your function should return `true`; otherwise, it should return `false`.

**Input**

```
characters = "Bste!hetsi ogEAxpelrt x ";
document = "AlgoExpert is the Best!";
```

**Output**

```
true
```

### Solution

**Walkthrough:**

- Create a hash map to count the frequency of it char from the `characters`.
- Loop through the `document` and check if the char is in the hash map.
- - If true: decrement the count of the char in the hash map.
- - If false: return false, because we can't generate the document.

**Complexity:**

- Time = O(n + m): Lenght of characters + lenght of document.
- Space = O(c): The number of unique characters in the `characters` string. If were only alphabetical characters, we would have 26 unique characters.

**Code:**

```js
function generateDocument(characters, doc) {
  const chars = {};

  for (c of characters) chars[c] = chars[c] + 1 || 1;

  for (c of doc) {
    if (!chars[c]) return false;
    chars[c] = chars[c] - 1;
  }

  return true;
}
```
