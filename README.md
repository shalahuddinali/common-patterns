# Common Pattern Solving Method

## Frequency Counter

**Sample Problem**: Write a function, which accepts two arrays. The function should return true if every value in the array has it's corresponding value squared in the second array.The frequency of values must be the same.

```javascript
function same(arr1, arr2) {
	if (arr1.length !== arr2.length) return false;

	let frequencyCounter1 = {};
	let frequencyCounter2 = {};

	for (let val of arr1) {
		frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1;
	}

	for (let val of arr2) {
		frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1;
	}

	for (let key in frequencyCounter1) {
		if (!(key ** 2 in frequencyCounter2)) return false;
		if (frequencyCounter2[key ** 2] !== frequencyCounter1[key]) return false;
	}

	return true;
}

same([1, 2, 3, 2, 5], [9, 1, 4, 4, 11]);
```

**Sample Problem**: Given two strings, write a function to determine if the second string is an anagram of the first. An anagram is a word, phrase, or name formed by rearranging the letters of another,such as _cinema_,formed from _iceman_

```javascript
function anagram(str1, str2) {
	if (str1.length !== str2.length) return false;

	let refObj = {};

	for (let val of str1) {
		refObj[val] = (refObj[val] || 0) + 1;
	}

	for (let val of str2) {
		if (!refObj[val]) return false;
		refObj[val]--;
	}

	return true;
}

anagram('catttr', 'tacttt');
```
# common-patterns
