---
description: >-
  By picking an item in an array to pivot on, we move everything less than the
  pivot to the left of it, and then the pivot is in the correct position. The
  process is then repeated.
---

# Quick Sort

It's important to note that "quick sort" is more like a family of algorithms that all share the same pattern. While you're carrying out research on quick sort, you may start to ask yourself the question: "Why is every quick sort implementation I see different?" - and it usually comes down to the fact that the first step, picking a pivot point, can be done in many ways.

* pick the first item
* pick the last item
* pick a random item
* pick the middle item
* pick the median item using a separate algorithm to find it

Depending on the strategy you end up using to pick a pivot, will determine "how" this algorithm looks when you visualise it.

The main example here **picks the first item as the pivot** because it's easiest to visualise. (this is not necessarily the best pivot to pick, which will be discussed later when it comes to trying to avoid worst case scenarios).

One thing to note is this algorithm happens 'in place'. There are some implementations online that create new arrays and combine them back together but the true implementation of Quick Sort operates on the original array.

In English:\
\- we pick an item in the array to act as the first 'pivot'.\
\- We iterate through the array, looking for the numbers that are left than the pivot, if we find one we initially swap it with the number to the right of the pivot.\
\- Once we've completed our search for lower numbers we 'leapfrog' the pivot number over all the lower numbers so it lands in the correctly sorted position.\
\- The process is repeated for numbers on the left and numbers on the right of the original pivot item.\


Given the array \[2,5,3,9,6,1,7,4] (for this example we'll start with the first item as the pivot point)\
\
**First pass**\
****\[<mark style="color:blue;">2</mark>, 5, 3, 9, 6, 1, 7, 4] -> we then iterate through the array comparing with the pivot to find lower \
\[<mark style="color:red;">2, 5</mark>, 3, 9, 6, 1, 7, 4]\
\[<mark style="color:red;">2</mark>, 5, <mark style="color:red;">3</mark>, 9, 6, 1, 7, 4]\
\[<mark style="color:red;">2</mark>, 5, 3, <mark style="color:red;">9</mark>, 6, 1, 7, 4]\
\[<mark style="color:red;">2</mark>, 5, 3, 9, <mark style="color:red;">6</mark>, 1, 7, 4]\
\[<mark style="color:red;">2</mark>, 5, 3, 9, 6, <mark style="color:red;">1</mark>, 7, 4] -> \[<mark style="color:red;">2</mark>,<mark style="color:orange;">1</mark>,3,9,6,<mark style="color:orange;">5</mark>,7,4] -> swap with number right of pivot\
\[<mark style="color:red;">2</mark>, 1, 3, 9, 6, 5, <mark style="color:red;">7</mark>, 4]\
\[<mark style="color:red;">2</mark>, 1, 3, 9, 6, 5, 7, <mark style="color:red;">4</mark>] -> we now check how many items we swapped (in this case 1 item)\
\[1, <mark style="color:green;">2</mark>, 3, 9, 6, 5, 7, 4] <- So the value 2, is moved past that 1 item and is now correctly sorted.\
\
**Second pass**\
****\[<mark style="color:red;">1</mark>, <mark style="color:green;">2</mark>, 3, 9, 6, 5, 7, 4] <- we would then repeat the process for the left side of the value 2, but there's only 1 item so it's already sorted.\
\
**Third pass**\
****\[<mark style="color:green;">1</mark>, <mark style="color:green;">2</mark>, <mark style="color:green;">3</mark>, 9, 6, 5, 7, 4] <- we would go through the process with the value 3 as the pivot point, however as there are no numbers less than three it doesn't move and is in its correctly sorted position. Our algorithm would then repeat the process for the left of 3, but in this case there is nothing to sort left of 3 so we move on to the right of 3.\
\
**Fourth pass**\
****\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:red;">6</mark>, 5, 7, 4] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, 5, 7, 4] -> move 6 to right of pivot (although it's already there)\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, 6, <mark style="color:red;">5</mark>, 7, 4] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, <mark style="color:blue;">5</mark>, 7, 4] -> move 5 to the right of 6 (although it's already there)\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, 6, 5, <mark style="color:red;">7</mark>, 4] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, <mark style="color:blue;">5</mark>, <mark style="color:blue;">7</mark>, 4] -> same as above\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, 6, 5, 7, <mark style="color:red;">4</mark>] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, <mark style="color:blue;">5</mark>, <mark style="color:blue;">7</mark>, <mark style="color:blue;">4</mark>] -> by the end there are four values less than 9\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:orange;">9</mark>, 6, 5, 7, <mark style="color:orange;">4</mark>] -> \[<mark style="color:green;">1, 2, 3</mark>, 4, 6, 5, 7, <mark style="color:green;">9</mark>] -> the value 9 moves to this index position and is sorted\
\
**Fifth pass**\
****\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">4</mark>, <mark style="color:red;">6</mark>, 5, 7, <mark style="color:green;">9</mark>] -> repeating the process for everything left of the value 9\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">4</mark>, 6, <mark style="color:red;">5</mark>, 7, <mark style="color:green;">9</mark>]\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">4</mark>, 6, 5, <mark style="color:red;">7</mark>, <mark style="color:green;">9</mark>]\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, 6, 5, 7, <mark style="color:green;">9</mark>] -> nothing lower than 4 so nothing moves and 4 is sorted\
The algorithm looks to work with the left side of 4, but there's nothing there to be sorted, so looks to the right side of 4\
\
**Sixth pass**\
****\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, <mark style="color:red;">6</mark>, <mark style="color:red;">5</mark>, 7, <mark style="color:green;">9</mark>] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, <mark style="color:red;">6</mark>, <mark style="color:blue;">5</mark>, 7, <mark style="color:green;">9</mark>] -> There is one item less than 6\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, <mark style="color:red;">6</mark>, 5, <mark style="color:red;">7</mark>, <mark style="color:green;">9</mark>] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, <mark style="color:red;">6</mark>, <mark style="color:blue;">5</mark>, 7, <mark style="color:green;">9</mark>]\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, <mark style="color:orange;">6</mark>, <mark style="color:orange;">5</mark>, 7, <mark style="color:green;">9</mark>] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, 5, <mark style="color:green;">6</mark>, 7, <mark style="color:green;">9</mark>] -> 6 is now in its sorted position.\
\
The algorithm would then work with the left side of 6, find there's only 1 item and that's sorted.\
And the same with the right side.\
\
**End**\
****\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:green;">4</mark>, <mark style="color:green;">5</mark>, <mark style="color:green;">6</mark>, <mark style="color:green;">7</mark>, <mark style="color:green;">9</mark>]\


To start we're going to use a helper function called partition which will complete one pass by:\
\- Selecting a starting pivot\
\- Carrying out comparisons on the array items being looked at. \
\- Carry out swaps where necessary\
\- Move the item at the pivot point to its new (and correctly sorted place)\
\- Return the pivot index\
\
The main Quick Sort function will use the pivot point to recursively execute on the items to the left of the pivot point, and the items to the right of the pivot point. At the point where the left and right pointers are the same, then there are no more items to compare. Here's a JavaScript implementation.

```javascript
//JavaScript

function partition(arr, start, end) {
  let pivot = arr[start];
  let swapIndex = start;
  for (let i = start + 1; i <= end; i++) {
    if (arr[i] < pivot) {
      swapIndex++;
      const temp = arr[swapIndex];
      arr[swapIndex] = arr[i];
      arr[i] = temp;
    }
  }
  const temp = arr[start];
  arr[start] = arr[swapIndex];
  arr[swapIndex] = temp;
  
  return swapIndex;
}

/*
Takes the arr, and a start and end value so it knows which items to loop through.
The swapIndex variable keeps track of how many swaps were made, so it can know where
to finally place the pivot item. It returns this value to the main function.
*/
```

This quickSort function takes an array, a left value and a right value and runs the pivot helper function over the array items in a range. It does this recursively, as the values to the left and right decrease. When the left and right values meet then there's nothing left to sort so it will return the array. Again, like merge sort, the trickiest thing to wrap your head around here is the recursive nature.

```javascript
//JavaScript
//This makes use of JS's ability to have default parameters

function quickSort(arr, left = 0, right = arr.length - 1) {
  if (left < right) {
    let pivotIndex = partition(arr, left, right);
    quickSort(arr, left, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, right);
  }

  return arr;
}
```

Note: Quick sort is an in-place algorithm. You may see some implementations online that use a slice method to take the left and right sections, and ultimately combine these new arrays back together. As that implementation creates new arrays it would no longer in-place and not really a proper quick sort.

BigO\
Best and average case are O(n log n) but worst case is O(n^2)

The worst case comes if we're given an already-sorted array and picking the first item as the pivot! We would have to go through and swap every item in the array, again and again etc. We can get around this by picking the middle element as the initial pivot.\


### Additional

Here's an implementation of Quick Sort which takes the middle item as the pivot.

Given the array \[2,15,3,9,6,1,7,14] (for this example we'll start with the middle item as the pivot point)\
\
**First pass**

\[2, 15, 3, <mark style="color:red;">9</mark>, 6, 1, 7, 14] \
for this implementation we use the multiple pointer pattern (call them i and j) to help move the items smaller than 9 to the left and items greater than 9 to the right. i starts at the first item and j starts at the last item\
\
\[<mark style="color:red;">2</mark>, 15, 3, <mark style="color:red;">9</mark>, 6, 1, 7, 14]\
&#x20;i                               j\
\
Starting with the i pointer, we compare the value at i to the pivot value (in this case 9), if it's less than then we leave it (because it's on the correct side of 9) and we increment i\
\
\[2, <mark style="color:red;">15</mark>, 3, <mark style="color:red;">9</mark>, 6, 1, 7, 14]\
&#x20;     i                          j\
\
Now comparing the value at i (15), we see it is larger than 9, and so not on the correct side!! Now we use j to find a value we can swap 15 with (ie, we need to find a value on the right side that shouldn't be there!)\
\
\[2, 15, 3, <mark style="color:red;">9</mark>, 6, 1, 7, <mark style="color:red;">14</mark>] Comparing 14 to 9, that's in the correct place so we decrement j\
&#x20;      i                         j\
\
\[2, 15, 3, <mark style="color:red;">9</mark>, 6, 1, <mark style="color:red;">7</mark>, 14]\
&#x20;     i                     j

Comparing 7 to 9, we can see that it's less than and therefore not on the correct side of 9. We've found something to swap 15 with!! so we do that, and increment i + decrement j straight after.\
\
\[2, 15, 3, <mark style="color:red;">9</mark>, 6, 1, <mark style="color:red;">7</mark>, 14] -> \[2, <mark style="color:green;"></mark> <mark style="color:blue;">7</mark>, 3, <mark style="color:red;">9</mark>, 6, 1, <mark style="color:blue;">15</mark>, 14] -> \[2, 7, 3, <mark style="color:red;">9</mark>, 6, 1, 15, 14]\
&#x20;      i                    j                  i                     j                       i           j\
\
\[2, 7, 3, <mark style="color:red;">9</mark>, 6, 1, 15, 14] Comparing 3 to the pivot, it is fine so increment i\
&#x20;         i           j\
\
\[2, 7, 3, <mark style="color:red;">9</mark>, 6, 1, 15, 14] Comparing 9 to itself, it's not greater than so we move on to j\
&#x20;             i       j\
\
\[2, 7, 3, <mark style="color:red;">9</mark>, 6, 1, 15, 14] Comparing 1 to the pivot it's less than so we can swap with 9\
&#x20;             i       j\
\
\[2, 7, 3, 1, 6, <mark style="color:red;">9</mark>, 15, 14] Back with i, we see 6 is less than pivot so we increment i\
&#x20;                ij\
\
\[2, 7, 3, 1, 6, <mark style="color:red;">9</mark>, 15, 14] When i and j have crossed we stop, as i has found the correctly sorted pivot\
&#x20;                j    i\
\
We have now successfully placed all the smaller numbers to the left of 9, and all the greater numbers to the right. We can then run this algorithm recursively on the left and right sides until everything is sorted! Here's a JavaScript implementation of the plain english description above:\


```javascript
//JavaScript

/*
  This partition function does what was explained in english above.
  At the end we return i, to tell the main function where the pivot is
*/

function partition(arr, left, right) {
  let pivot = arr[Math.floor((right + left) / 2)];
  
  let i = left;
  let j = right;

  while (i <= j) {
    while (arr[i] < pivot) {
      i++;
    }
    while (arr[j] > pivot) {
      j--;
    }

    if (i <= j) {
      const temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
      i++;
      j--;
    }
  }
  return i;
}
```

```javascript
//JavaScript

function quickSort(arr, left, right) {
  if (arr.length > 1) {
    let i = partition(arr, left, right);
    
    //if there are items to sort on the left
    if (left < i - 1) {
      quickSort(arr, left, i - 1);
    }
    
    //if there are items to sort on the right
    if (i < right) {
      quickSort(arr, i, right);
    }
  }
  return arr;
}
```
