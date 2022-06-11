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
    this.first = current?.next!;
    this.size--;

    return current;
  }
}
```
