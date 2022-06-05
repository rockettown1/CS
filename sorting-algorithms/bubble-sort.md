# Bubble Sort

The largest value will bubble to the top. We pass through the array comparing pairs and if the item on the left is larger we swap (visualising an array from left to right for example). After the first pass through the array, the largest item will be at the end (in its sorted position).&#x20;

We then continue this process making more passes through the array, each time ignoring the previously sorted larger items.

Given the array \[ 2, 6, 1, 7, 3]\
**First pass**\
****\[ <mark style="color:red;"></mark> <mark style="color:red;"></mark><mark style="color:red;">**2, 6**</mark>, 1, 7, 3] -> no swap\
\[ 2, <mark style="color:red;">**1, 6**</mark>, 7, 3] -> swap\
\[ 2, 1, <mark style="color:red;">**6, 7**</mark>, 3] -> no swap\
\[ 2, 1, 6, <mark style="color:red;">**3,**</mark><mark style="color:red;">** **</mark><mark style="color:red;"><mark style="color:green;">**7**<mark style="color:green;"></mark>] -> swap (the value 7 is now in its correctly sorted place)\
\
**Second pass**\
\[ <mark style="color:red;">**1, 2**</mark>, 6, 3, 7] -> swap\
\[ 1, <mark style="color:red;">**2, 6**</mark>, 3, 7] -> no swap\
\[ 1, 2, <mark style="color:red;">**3,**</mark>**  **<mark style="color:red;">**6**</mark><mark style="color:red;">,</mark> <mark style="color:green;">7</mark>] -> swap (the value 6 is now in its correctly sorted place)\
\
**Third pass**\
****\[ <mark style="color:red;">**1, 2**</mark>, 3, 6, 7] -> no swap\
\[ 1, <mark style="color:red;">**2, 3**</mark>, <mark style="color:green;">6, 7</mark>] -> no swap (the value 3 is now in its correctly sorted place)\
\
**Fourth pass**\
****\[ <mark style="color:red;">**1, 2**</mark>, <mark style="color:green;">3, 6, 7</mark>] -> no swap (the value 2 is now in its correctly sorted place)\
\
**End**\
\[ <mark style="color:green;">1, 2, 3, 6, 7</mark>] -> all values now sorted



Given an array of n integers:

* The first pass through the array we want to carry out n - 1 comparisons (we don't compare the last item with anything).
* The second pass through we want to carry out n - 2 comparisons (for the same reason as above, but also from the previous pass we have an item already sorted so we don't need to look at it). etc etc
* We can control the number of comparisons by reducing the number of times the outer loop executes. So we can start i at the last index and work our way down to an index of 1.
* With the inner loop we are basically comparing an item and the one next to it for the amount of times the outer loop specifies.&#x20;

```javascript
//JavaScript (Iterative)

function bubbleSort(arr){
   for (let i = arr.length - 1; i > 0; i--) {
    for (let j = 0; j < i; j++) {
      if (arr[j] > arr[j + 1]) {
        const temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

Just for comparison purposes, here's the recursive implementation written in JavaScript.

```javascript
//JavaScript (Recursive)

function bubbleSort(arr, length) {
  if (length == 1) return arr;

  for (let j = 0; j < length - 1; j++) {
    if (arr[j] > arr[j + 1]) {
      const temp = arr[j];
      arr[j] = arr[j + 1];
      arr[j + 1] = temp;
    }
  }

  return bubbleSort(arr, length - 1);
}

bubbleSort(arr, arr.length)
```

There is an optimisation we can make to bubble, which involves keeping track of whether a swap occurred. If you imagine a situation where we have a nearly-sorted array, the code will continue to loop through until it's compared everything. \
\
If you look at the example at the very top of this page, there was no reason we carried out the fourth pass, because no swaps occurred on the third pass! If we can know this information we can tell our algorithm to end without needing to do any more passes. Here's the additional code we can add to our algorithm (added to the iterative implementation but you can make the same modification to the recursive version):

```javascript
//JavaScript (Iterative)

function bubbleSort(arr){
   let swaps; //outside of loop so not declaring a new variable each loop
   for (let i = arr.length - 1; i > 0; i--) {
   swaps = false // assign false initially as the loop starts
    for (let j = 0; j < i; j++) {
      if (arr[j] > arr[j + 1]) {
        const temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
        swaps = true // assign true if a swap has occured
      }
    }
    if (!swaps) break // if it was never assigned true, break out.
  }
  return arr;
}
```

#### BigO

Generally average case is O(n^2) for time complexity. For best cases (nearly sorted) it would be O(n) but it's rare to come across best case scenarios.
