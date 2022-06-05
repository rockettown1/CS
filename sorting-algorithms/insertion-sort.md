---
description: >-
  Builds up the sort by gradually increasing the portion of array we are
  operating on. It takes each element and inserts it where it should be in the
  already sorted portion of the array.
---

# Insertion Sort

In english:

* Start with the second item and compare it to the first item (the first item starts as the 'sorted section').&#x20;
* Store the value of the item we're comparing with
* **Compare the item to the one before it** and if its smaller, then move the one before it into the slot for our stored value.
* Continue to the next element, if its in the wrong order we **iterate through the sorted section (ie everything to the left of the element)** to find its correct spot.
* Once you've found a value that is less than the stored value, insert the stored value at the correct index position.
* As we move through the array, the sorted part grows until it encompasses all of the array&#x20;



Given the array \[ 2, 6, 1, 7, 3]:

**First pass:** (starting at second item - comparing the value 6)\
\[ <mark style="color:red;">2, 6</mark>, 1, 7, 3] -> no move\
\
**Second pass** (starting at third item - comparing the value 1)\
\[ 2, 6<mark style="color:red;">, 6</mark>, 7, 3] -> move 6 into the index for third item\
\[ <mark style="color:red;">1, 2</mark>, 6, 7, 3] -> move 2 into the index for second item and INSERT 1 into the first index\
&#x20; ^   \
**Third pass** (starting at fourth item - comparing the value 7)\
\[ <mark style="color:green;">1, 2</mark>, <mark style="color:red;">6, 7</mark>, 3] -> no move\
\
**Fourth pass** (starting at fifth (final) item - comparing the value 3)\
\[ <mark style="color:green;">1, 2</mark>, 6, 7<mark style="color:red;">, 7</mark>] -> move 7 into the fifth spot\
\[ <mark style="color:green;">1, 2</mark>, 6<mark style="color:red;">, 6</mark>, 7] -> move 6 into the fourth spot\
\[ <mark style="color:green;">1, 2, 3</mark>, 6, 7] -> when 3 is compared to 2, there's no move so we INSERT 3 into that index position.\
&#x20;         ^ \
**End**\
****\[ <mark style="color:green;">1, 2, 3, 6, 7</mark>] -> all items in correct order\


```javascript
//JavaScript (Iterative)

//I've seen a few different implementations of this. DYOR

function insertionSort(arr){
    for (let i = 1; i < arr.length; i++) {
            let current = arr[i];
            let j = i-1; 
            while ((j >= 0) && (current < arr[j])) {
                arr[j+1] = arr[j];
                j--;
            }
            arr[j+1] = current;
        }
    return arr;
}
```

### Discussion

Although it is one of the elementary sorting algorithms with O(n^2) worst-case time, insertion sort is the algorithm of choice either when the **data is nearly sorted** (because it is adaptive) or when the problem size is small (because it has low overhead).

For these reasons, and because it is also stable, insertion sort is often used as the recursive base case (when the problem size is small) for higher overhead divide-and-conquer sorting algorithms, such as merge sort or quick sort.

Remember to check out the links on [sorting-background-info.md](sorting-background-info.md "mention")to visualise this algorithm. It will help when understanding the implementation.

