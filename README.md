# Common Pattern Solving Method

## Frequency Counter

- This pattern uses objects or sets to collect values/frequencies of values to avoid the need for nested loops.

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

## Multiple Pointers

- Creating pointers or values that correspond to an index or position and move towards the beginning,end or middle based on certain condition.
- Very efficient for solving problems with minimal space complexity as well

**Sample Problem**: Write a function, which accepts a **sorted** array of intergers. The function should find the **first** pair where the sum is 0. Return an array that includes both values that sum to zero or undefined if a pair does not exist.

```javascript
function sumZero(arr) {
	let left = 0;
	let right = arr.length - 1;

	while (left < right) {
		let sum = arr[left] + arr[right];

		if (sum === 0) return [arr[left], arr[right]];

		sum > 0 ? right-- : left++;
	}
}

sumZero([-4, -3, -2, -1, 0, 1, 2, 3, 4]);
```

**Sample Problem**: Implement a function which accepts a sorted array, and counts the unique values in the array, There can be negative numbers in the array, but it will always be sorted.

```javascript
function countUniqueValues(arr) {
	if (arr.length === 0) return 0;
	let i = 0;

	for (let j = 1; j < arr.length; j++) {
		if (arr[i] !== arr[j]) {
			i++;
			arr[i] = arr[j];
		}
	}
	return i + 1;
}

countUniqueValues([1, 3, 4, 5, 5, 5, 6, 7, 7]);
```

## Sliding Window

- This pattern involves creating a **window** which can either be an array or a number from one position to another.
  Depending on a certain condition, the window either increases or closes(and a new window created)
- Very useful for keeping track of a subset of data in an array/string etc.

**Sample Problem**: Write a function, which accepts an array of intergers and a number called **n**. The function should calculate the maximum sum of **n** consecutive elements in the array.

```javascript
function maxSubarraySum(arr, num) {
	let maxSum = 0;
	let tempSum = 0;
	if (arr.length < num) return null;
	for (let i = 0; i < num; i++) {
		maxSum += arr[i];
	}
	tempSum = maxSum;
	for (let i = num; i < arr.length; i++) {
		tempSum = tempSum - arr[i - num] + arr[i];
		maxSum = Math.max(maxSum, tempSum);
	}
	return maxSum;
}

maxSubarraySum([2, 6, 9, 2, 1, 8, 5, 6, 3], 3);
```
