---
description: Discard half the data on each iteration (only works with sorted data)
---

# Binary Search

Choose the middle element of an array and do a comparison on whether the value we're looking for is equal to, before or after the middle element picked. Based on whether it's before or after determines which part of the array we search next, effectively cutting the number of items needed to search in half on each iteration. This is an example of divide and conquer.

Binary search works by using the two pointers at either end of an array (or sub array) and dividing the search window in half each iteration.&#x20;

1. Start with a left pointer (index of first item) and a right pointer (index of last item).
2. Find the index of an item in the middle of these two initial pointers.
3. Use that middle index to compare the value in the middle of the array with the one you're trying to find.
4. If the middle value is greater than the searched for value, move the right pointer to the middle - 1 (focusing on the first half of the array), if the middle value is less than the searched for value, move the left pointer to the middle + 1 (focusing on the second half of the array).
5. Find a new middle value and repeat the process with the new values for either left or right.&#x20;
6. If the searched for value is actually in the array, then at some point the middle value picked will be the one you're looking for.
7. If the searched for value doesn't exist in the array, then at some point the left and right pointers will meet or cross, at which point we can declare that no such value exists and we return -1.

Here's a good visualisation of how binary search works. Just input a value in the top left and select binary search.

{% embed url="https://www.cs.usfca.edu/~galles/visualization/Search.html" %}

```javascript
// JavaScript (Iterative implementation)

function binarySearch(arr, val){
  //pointer indices
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    let middle = Math.round((left + right) / 2);
    if (val == arr[middle]) return middle;

    //update left or right pointer
    if (val < arr[middle]) right = middle - 1;
    else left = middle + 1;
  }
  return -1;
}
```

```javascript
// JavaScript (Recursive implementation)

function binarySearch(arr, val, left, right) {
  if (left <= right) {
    let middle = Math.round((left + right) / 2);

    if (val == arr[middle]) {
      return middle;
    }
    if (val < arr[middle]) {
      return binarySearch(arr, val, left, middle - 1);
    } else {
      return binarySearch(arr, val, middle + 1, right);
    }
  }
  return -1;
}


// base cases: 
// left > right return -1
// val = arr[middle] return middle
```

### BigO (time complexity)

Note: Logs are base 2.

To understand why its log n, think of how many steps it would take to get an answer.

* Say you have an array of 2 items, you would only need to run this algorithm 1 time to get an answer.
* If you had an array of 4 items, you would need to run it 2 times
* If you had an array of 8 items, you would need to run it 3 times
* if you had an array of 16 items, you would need to run it 4 times
* if you had an array of 32 items, you would need to run it 5 times

So as the number of items (n) in the array doubles, the number of operations (x) increases by 1. Or more generally, as n grows, the time it takes increases by log n.

Below are the steps of how we get from the first mathematical relationship to the bottom one. If you've never studied maths before it might be worth looking up the log relationships but the general idea is that log(base 2) multiplied by 2 = 1. So in the middle step you bring the exponent down to the front and the log cancels out on the left hand side.

Starting with $$2^x = n$$ we log both sides $$log 2^x = log n$$&#x20;

Moving the exponent down $$xlog 2 = log n$$ and because log2 = 1 we arrive at $$x = log n$$

So the number of operations (ie the time it takes) is equal to the log of the input size.



| Best                    | Average  | Worst    |
| ----------------------- | -------- | -------- |
| O(1)                    | O(log n) | O(log n) |
| Find item straight away |          |          |
