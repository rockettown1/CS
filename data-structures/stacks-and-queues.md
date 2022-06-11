---
description: A stack is LIFO and a queue is FIFO
---

# Stacks & Queues

For a stack, imagine a deck of cards you are placing on a table one after the other.\
If you want to remove a card from the 'stack' you can only remove the last one you put down (from the top of the pile). Last In First Out.

For a queue, just imagine a queue you might come across in everyday life, (like in Starbucks). Who ever joins the queue first, will leave the queue first (after making their order for example). First In First Out.

### Stacks

Examples of places you might come across use of stacks as a developer include, the call stack (when executing nested functions for example), keeping track of undoing/redoing with ctrl Z, or the history object / routing in the browser.

#### Creating a stack with an array

```typescript
let stack = []
stack.push("Google")
stack.push("Instagram")

stack.pop()
```

To adhere to the stack concept, we can only push and pop from the end.&#x20;

#### Creating a stack with a linked list

The preferred method of implementing a stack is with a linked list (as we don't need a lot of the benefits arrays offer, such as random access). However, because adding and removing items from our stack should execute in **constant time O(1)** we can't use the push and pop methods previously implemented (because to get to the end, we'd need to traverse the entire list to get there!)

Instead we use the shift and unshift methods (add and remove from the start) but we will rename them push and pop to adhere to convention. Here's a class implementation of stack written in TypeScript. (Note, it's just a linked list really).

```typescript
//helper class to make new Node objects
class Node {
  public next: Node | null;
  constructor(public val: any) {
    this.val = val;
    this.next = null;
  }
}

class Stack {
  first: Node | null;
  last: Node | null;
  size: number;

  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  public push(val: any) {
    let newFirst = new Node(val);
    if (!this.first) {
      this.first = newFirst;
      this.last = newFirst;
    } else {
      newFirst.next = this.first;
      this.first = newFirst;
    }
    this.size++;
    
    return this.size;
  }

  public pop() {
    if (this.size === 0) return null;
    let current = this.first;
    
    if (this.first === this.last) {
      this.last = null;
    }
    
    this.first = current?.next!;
    this.size--;

    return current;
  }
}
```

### Queues

Very similar to a stack but first in first out (like a print queue on a printer). Like with a stack, it's an abstract concept and there are multiple ways to implement the idea. You could use an array, but like above, you'd get a load of extra stuff that comes with arrays that just isn't needed, so it's usually preferred to implement a queue manually using a linked list.

If we were using an array we could add to the start and remove from the end (using the unshift and pop methods in JS/TS). Remember thought with arrays, adding to the start means the entire array will then need re-indexing (expensive depending on the size of the array).

#### Implementing a Queue with a linked list.

To keep it constant time O(1) we add to the end and we remove from the beginning. Here we call them enqueue and dequeue but they are just the same push and shift methods from a linked list.

```typescript
class Node {
  public next: Node | null;
  constructor(public val: any) {
    this.val = val;
    this.next = null;
  }
}

class Queue {
  first: Node | null;
  last: Node | null;
  size: number;

  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  
public enqueue(val: any) {
    const node = new Node(val);

    if (!this.first) {
      this.first = node;
      this.last = this.first;
      this.size = 1;
    } else {
      this.last!.next = node;
      this.last = node;
      this.size++;
    }
    return this;
  }

  public dequeue() {
    if (this.size === 0) return null;
    let current = this.first;
    if (this.first === this.last) {
      this.last = null;
    }

    this.first = current?.next!;
    this.size--;

    return current;
  }
  
}
```

