---
description: Given a sorted array, return two numbers that sum to zero.
---

# SumZero

#### Examples

\[-3, -2, 1, 1, 2, 3] -> \[-3, 3]\
\[-2, 1, 0, 3, 4] -> undefined



The naive solution is to loop through the array for each item in the array (nested for loops). So take the first number, and loop through the array looking for a second number that sums to zero. \
This is obviously not great from a time complexity O(n^2) because for an array of length n, the number of operations increases by n^2. NOTE: This solution just returns the first pair it finds, if the problem asks for all pairs then it should be modified.\


#### Naive solution O(n^2) - quadratic time

```javascript
const sumZero = (arr) => {
    for (let i = 0; i < arr.length; i++){
        for (let j = i+1; j < arr.length; j++){
            if (arr[i] + arr[j] === 0){
                return [arr[i], arr[j]]
            }
        }
    }
}
```

#### Better solution O(n) - linear time

We can use the multiple pointers pattern to avoid nested for-loops. We keep track of the item at the start and the end of the array (smallest and largest because the array is sorted), and we sum the two values. If the sum is too large (greater than zero), we move the end pointer left by one (decrease the pointers index) and if the sum is too small (less than zero) we move the start pointer right by one (increase the pointers index) - each time summing the two values looking for zero. Finally we stop looping if the two pointers cross over (ie the left pointer becomes greater or equal to the right pointer)\


```javascript
const sumZero = (arr) => {
    let left = 0 //index of the first item
    let right = arr.length - 1 //index of the last item
    while (left < right) {
        let sum = arr[left] + arr[right]
        if (sum === 0) {
            return [arr[left] + arr[right]]
        } else if (sum > 0){
            right--
        } else {
            left++
        }
    }
}
```

#### Another solution using a hash map O(n) - linear time

This solution basically loops through the array once, and for each item checks or inserts into a hash map. The key (of the key value pair) is the value that we would need to sum to zero, and as we continue through the array if we find that value we must have found a matching pair that sum to zero. \
\
For example if the current value in the array is -2, we:\
\- check whether there is a key in the hash map of -2\
\- if not, we store that value with the key of what would sum to zero { 2: -2 }\
\- as we continue through the array, if we find the number 2, and hashMap\[2] exists, we must have come across -2 earlier in the process, in which case we've found a pair. \
\
The solution below finds all pairs and returns an array of all matches:

```javascript
const sumZero = (arr) => {
  const hashMap = {};
  const pairs = [];
  for (let num of arr) {
    if (num == 0) continue;

    if (!hashMap[num]) {
      hashMap[0 - num] = num;
    } else {
      pairs.push([hashMap[num], num]);
    }
  }
  return pairs;
};
```
