---
description: These code examples use JavaScript
---

# Problems and Examples

### Basic example

Let's compare a function first written iteratively, then written recursively, that takes a number and counts down (logs the number in the console) until it reaches 1.

```javascript
//Iterative

function countDown(num){
    for (let i = num; i > 0; i--){
        console.log(i)
    }
}
```

```javascript
//Recursive

function countDown(num){
    if (num === 0){ // <-- the base case (which stops it from calling itself)
        return
    }
    console.log(num)
    countDown(num - 1) // <-- a different input each time
}
```

### Other examples

Sum all the numbers between 1 and a given number (inclusive)

```javascript
//Iterative (using the accumlator pattern)

function sumRange(num){
    let total = 0
    for (let i = 1; i <= num; i++){
        total += i
    }
    return total
}
```

```javascript
//Recursive

function sumRange(num){
    if (num === 1) return 1 // <-- the base case
    
    return num + sumRange(num - 1) // <-- different input each time
}
```

Try to visualise the call stack in this example. The first function call invokes a second function call which will invoke a third etc etc until it hits a case where num == 1 (where instead of invoking anything it'll just return 1). Think about what the return value will be for each invocation. Let's look at each call but replacing the num variable with an actual int value for clarity.

```javascript
//PSEUDO CODE

//first function call
function sumRange(4){
    if (4 === 1) return 1 
    
    return 4 + 6 // the 6 comes from the return value of the second call
}

//section function call
function sumRange(4 - 1){
    if (3 === 1) return 1 
    
    return 3 + 3 // the 3 comes from the return value of the third call
}

//third function call
function sumRange(3 - 1){
    if (2 === 1) return 1 
    
    return 2 + 1 // the 1 comes from the return value of the fourth call
}

//fourth function call
function sumRange(2 - 1){
    if (1 === 1) return 1 // returns the base case!
    
    
}
```

Another way to visualise the above is you work your way down each call, then work your way back up with the return values. The fourth and final function call will be the one to finish executing first, and returning 1. The third function call will finish next returning 2 + the return value of the previous etc etc.

If you picture the call stack, 4 functions are added to the call stack one after the other and the one before it is waiting for the return value of the function call above it in the stack.&#x20;

#### Factorial

Making use of the fact that:\
factorial of 3 (1 \* 2 \* 3) is the same as (factorial of 1 \* factorial of 2 \* 3)

or in other words the number multiplied by the factorial of the number before it

So our factorial function needs to return the product of a number and the factorial before it, unless the number is 1 (no factorial before it) then it should just return 1.\


```javascript
//Iterative (using the accumulator pattern)

function factorial(num){
    let total = 1
    for (let i = num; i > 1; i--){
        total *= i
    }
    return total
}
```

```javascript
//Recursive

//Q. What is the base case?
//A. When we reach the factorial of 1. No more function calls needed.

function factorial(num){
    if (num === 1) return 1
    return num * factorial(num - 1)
}

```

### Where things can go wrong

* No base case\
  Functions will keep calling themselves, which means you'll reach the max call stack size (stack overflow).
* Forgetting to return or returning the wrong thing\
  Can also lead to a similar outcome has a missing base case



