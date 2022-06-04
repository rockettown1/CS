---
description: Discard half the data on each iteration (only works with sorted data)
---

# Binary Search

Chose the middle element and do a comparison on whether an item is before or after the chosen value. Then repeat this process until there's no more items to search with. This is an example of divide and conquer.

```javascript
// JavaScript

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
