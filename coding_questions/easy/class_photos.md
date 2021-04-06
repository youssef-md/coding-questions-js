## Class Photos

### Prompt
It's photo day at the local school, and you're the photographer assigned to take class photos. The class that you'll be photographing has an even number of students, and all these students are wearing red or blue shirts. In fact, exactly half of the class is wearing red shirts, and the other half is wearing blue shirts. You're responsible for arranging the students in two rows before taking the photo. Each row should contain the same number of the students and should adhere to the following guidelines:

- All students wearing red shirts must be in the same row.
- All students wearing blue shirts must be in the same row.
- Each student in the back row must be strictly taller than the student directly in front of them in the front row.
  
You're given two input arrays: one containing the heights of all the students with red shirts and another one containing the heights of all the students with blue shirts. These arrays will always have the same length, and each height will be a positive integer. Write a function that returns whether or not a class photo that follows the stated guidelines can be taken.

Note: you can assume that each class has at least 2 students.

**Input**
```js
redShirtHeights = [5, 8, 1, 3, 4]
blueShirtHeights = [6, 9, 2, 4, 5]
```

**Output**
```js
true // Place all students with blue shirts in the back row.
```

### Solution

__Walkthrough:__
- First let sort bouth arrays in descending order: `sortedReds` and `sortedBlues`.
- Create a flag to check if `isRedAdBack`(aka, if the taller student at `sortedReds` is > `sortedBlues[0]`).
- Loop through any array(they all must have the same sizes) and check if `isRedAtBack`
- - If true, then check if the current pair of [red, blue] student can't be togueter: `red <= blue`, if not return `false`.
- So if the `isRedAtBack` is false, then blue is at back, then check for the mismatch: `blue <= red`, if so return `false`.
- At the end of the loop if any pair of [red, blue] student had a mismatch, the loop would return `false`, so we can securely return `true` outside the loop.

__Complexity:__
- Time = O(n.log(n)): This is a greedy solution, we have the sort the arrays.
- Space = O(1): All the checks are inplace.

__Code:__

```js
function classPhotos(redShirtHeights, blueShirtHeights) {
  const sortedReds = redShirtHeights.sort((a, b) => b - a);
  const sortedBlues = blueShirtHeights.sort((a, b) => b - a);
  const isRedAtBack = sortedReds[0] > sortedBlues[0];
  
  for(let i = 0; i < sortedReds.length; i++) {
    if(isRedAtBack) {
      if(sortedReds[i] <= sortedBlues[i]) return false;
    }
  	else if(sortedBlues[i] <= sortedReds[i]) return false;				
  }
  
  return true;
}
```