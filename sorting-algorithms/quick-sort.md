---
description: >-
  By picking an item in an array to pivot on, we move everything less than the
  pivot to the left of it, and then the pivot is in the correct position. The
  process is then repeated.
---

# Quick Sort

Conceptually, this one is a little difficult to visualise. It will make use of recursion to repeat the "pick a pivot and move" process, so it's usually the recursion that catches people out.

One thing to note is this algorithm happens 'in place'. There are some implementations online that create new arrays and combine them back together but the true implementation of Quick Sort operates on the original array.

In English:\
\- we pick an item in the array to act as the first 'pivot' (this can be any number but as we'll discuss later some are better to pick than others to try and avoid worst case scenarios).\
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
****\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:red;">6</mark>, 5, 7, 4] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, 5, 7, 4] -> keeping track that 6 is less than 9\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, 6, <mark style="color:red;">5</mark>, 7, 4] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, <mark style="color:blue;">5</mark>, 7, 4]\
\[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, 6, 5, <mark style="color:red;">7</mark>, 4] -> \[<mark style="color:green;">1, 2, 3</mark>, <mark style="color:red;">9</mark>, <mark style="color:blue;">6</mark>, <mark style="color:blue;">5</mark>, <mark style="color:blue;">7</mark>, 4]\
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




\
