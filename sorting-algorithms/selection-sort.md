---
description: Similar to bubble sort but places small values first
---

# Selection Sort

This algorithm involves keeping track of the smallest value and comparing it to each item in the array. After one pass through the array we swap the smallest value with the first in the array (this is now in its sorted position). We then repeat the process this time starting from the next item in the array.

In pseudo code:\
\- Store the first element as the smallest value seen so far.\
\- Compare this item to the next item in the array until you find a smaller number.\
\- If a smaller number is found, designate that smaller number to be the new "min" and continue until the end of the array.\
\- If the "min" is not the value (index) you initially began with, swap the two values.

Given the array \[ 2, 6, 1, 7, 3]\
**First pass**\
****\[ <mark style="color:blue;">2</mark>, <mark style="color:blue;">6</mark>, 1, 7, 3] -> minimum is 2\
\[ <mark style="color:blue;">2</mark>, 6, <mark style="color:blue;">1,</mark> 7, 3] -> minimum is 1\
\[ 2, 6, <mark style="color:blue;">1, 7</mark>, 3] -> minimum is 1\
\[ 2, 6, <mark style="color:blue;">1</mark>, 7, <mark style="color:blue;">3</mark>] -> minimum is 1\
\[ <mark style="color:green;">1</mark>, 6, 2, 7, 3] <- swap 1 with first item we started with (value 1 is now in its sorted place)\
\
**Second pass**\
****\[ <mark style="color:green;">1</mark>, <mark style="color:blue;">6, 2</mark>, 7, 3] -> minimum is 2\
\[ <mark style="color:green;">1</mark>, 6, <mark style="color:blue;">2, 7</mark>, 3] -> minimum is 2\
\[ <mark style="color:green;">1</mark>, 6, <mark style="color:blue;">2</mark>, 7, <mark style="color:blue;">3</mark>] -> minimum is 2\
\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, 6, 7, 3] <- swap 2 with the first item we started with (value 2 is now in its sorted place)\
\
**Third pass**\
****\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:blue;">6, 7</mark>, 3] -> minimum is 6\
\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:blue;">6</mark>, 7, <mark style="color:blue;">3</mark>] -> minimum is 3\
\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:green;">3</mark>, 7, 6] <- swap 3 with the first item we started with (value 3 is now in its sorted place)\
\
**Fourth pass**\
****\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:green;">3</mark>, <mark style="color:blue;">7, 6</mark>] -> minimum is 6\
\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:green;">3</mark>, <mark style="color:green;">6</mark>, 7] <- swap 6 with the first item we started with (value 6 is now in its sorted place)\
\
**End**\
****\[ <mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:green;">3</mark>, <mark style="color:green;">6</mark>, <mark style="color:green;">7</mark>] <- all values sorted.

```javascript
//JavaScript (Iterative)

function selectionSort(arr){
    for (let i = 0; i < arr.length; i++) {
    let min = i;
    for (let j = i; j < arr.length - 1; j++) {
      if (arr[j + 1] < arr[min]) {
        min = j + 1;
      }
    }
    if (i !== min) {
      let temp = arr[i];
      arr[i] = arr[min];
      arr[min] = temp;
    }
  }
  return arr
}
```

#### BigO

Average case: O(n^2)
