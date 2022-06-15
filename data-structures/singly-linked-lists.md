---
description: >-
  Ordered list of data, but unlike arrays the data is not indexed. Instead each
  'node' has a value, and a pointer to the next 'node'.
---

# Singly Linked Lists

This data structure contains a head, tail and length property. Her's a linked list which stores the value 4, 6, 1 and 3.

<img src="../.gitbook/assets/file.drawing (2) (1).svg" alt="" class="gitbook-drawing">

{% embed url="https://visualgo.net/en/list" %}
Here's a great visualisation of working with a linked list
{% endembed %}

Creating, searching and removing items means we'll need to 'walk' through the linked list. So, unlike arrays, no random access is allowed.

#### Comparison with Arrays

| Linked List                             | Array                                                                         |
| --------------------------------------- | ----------------------------------------------------------------------------- |
| Do not have indexes                     | Indexed in order                                                              |
| Connected via nodes with a next pointer | Data is not connected but stored "together" in memory.                        |
| Random access is not allowed            | Random access (if you know the index)                                         |
| Insertion and deletion not expensive    | Insertion and deletion can be expensive because things need to be re-indexed. |

### Implementing a LinkedList Class

As the structure for a single Node and the list itself will not change each time we create them, we can create classes to represent these objects. The following implementation is in TypeScript but the general concepts will be the same most programming languages.&#x20;

```typescript
class Node {
  public next: Node | null
  
  constructor(public val: any) {
    this.val = val;
    this.next = null;
  }
}
```

A Node has two properties, the value it is storing, and the next property which will either be the next Node in the list, or null if there isn't one.

```typescript
class SinglyLinkedList {
  length: number;
  head: Node | null;
  tail: Node | null;

  constructor() {
    this.length = 0;
    this.head = null;
    this.tail = null;
  }

}

//create a new list
const myList = new SinglyLinkedList()
```

This class will get us started with an empty linked list. Each list will have three properties to keep track of: Its length (how many items are in the list), the head (the first item in the list) and the tail (the last item in the list). We can then implement methods to interact with our list:

* Push and Pop
* Shift and Unshift
* Get and Set
* Insert and Remove
* Reversing a linked list

### Push method

Add a value to the end of the list and reset the tail

```typescript

  public push(val: any) {
    const node = new Node(val);

    if (!this.head) {
      this.head = node;
      this.tail = this.head;
      this.length = 1;
    } else {
      this.tail!.next = node;
      this.tail = node;
      this.length++;
    }
    return this;
  }

```

### Pop method

Remove the last item from the list and reset the tail

```typescript

  public pop() {
    if (this.head == null) {
      return;
    }

    let current = this.head;
    let newTail = current;

    while (current?.next != null) {
      newTail = current;
      current = current.next;
    }
    this.tail = newTail;
    this.tail.next = null;
    this.length--;

    return this;
  }

```

### Shift method

Remove item from the beginning

```typescript

public shift() {
    if (!this.head) return undefined;

    let current = this.head;
    this.head = current?.next!;
    this.length--
    if (this.length === 0){
      this.tail = null
    }
    
    return current;
  }
```

### Unshift method

Add item to the beginning

```typescript

public unshift(val: any) {
    let newHead = new Node(val);
    if (!this.head) {
      this.head = newHead;
      this.tail = newHead;
    } else {
      newHead.next = this.head;
      this.head = newHead;
    }

    this.length++;
    return this
  }
```

### Get and Set methods

Get an item by passing an index, and setting a value at a particular index

```typescript
public get(index: number) {
  if (index < 0 || index >= this.length) return null;
  let current = this.head;
  for (let i = 0; i < index; i++) {
    current = current?.next!;
  }
  return current?.val;
}
  
 public set(val: any, index: number){
  let foundNode = this.get(index)
  if (foundNode){
    foundNode.val = val
    return true
  }
  return false
}
```

### Insert method

Insert a new node at a given index

```typescript
public insert(val: any, index: number) {
    if (index < 0 || index > this.length) return false;
    const newNode = new Node(val);
    newNode.val = val;
    if (index === this.length) {
      this.push(val);
      return true;
    }
    if (index === 0) {
      this.unshift(val);
      return true;
    }
    newNode.next = this.get(index);
    this.get(index - 1)!.next = newNode;
    this.length++;
    return true;
  }
```

### Remove method

Remove a node at a given index

```typescript
public remove(index: number) {
    if (index < 0 || index > this.length) return undefined;
    if (index === this.length - 1) return this.pop();
    if (index === 0) return this.shift();
    let prev = this.get(index - 1);
    let nodeToRemove = this.get(index);
    prev!.next = nodeToRemove!.next;
    this.length--
    return nodeToRemove;
  }
```

### Reversing a Linked List

This is a very common interview question. It's a little hard to wrap your head around if you're new to linked lists but here's an implementation in TypeScript which I'll talk through after.

```typescript
  public reverse() {
    let node = this.head;
    this.head = this.tail;
    this.tail = node;
    let next: Node | null;
    let prev = null;

    for (let i = 0; i < this.length; i++) {
      next = node!.next;
      node!.next = prev;
      prev = node;
      node = next;
    }

    return this
  }
```

<img src="../.gitbook/assets/file.drawing (1) (1) (1).svg" alt="" class="gitbook-drawing">

In English:\
So we start by swapping the head and the tail. Making use of a temp variable to keep track of the current node we are looking at in the loop.\
\
**First pass**\
\- We set the next property on the node to equal prev (initially null), so the first node points to null.\
\- We then change prev to equal node and node to equal next, before starting the loop again.\
\
**Second  pass**\
****- **** We update the next variable to hold a reference to the next node in the list (because we're about to sever the connection!)\
\- We then change the current node's next property to point to the prev node (which we set in the first pass). \
\- we then update the prev to equal the current node, and set the node to the stored next node\
\
**Third pass**\
****- Same as previous pass\
\- Store the next node in a variable\
\- Set the node's next property to equal the previous node\
\- Prepare for the next pass: Update the prev to equal the current node, updated the node to equal the next node.\
\
This is repeated for each item in the list (determined by the lists length in the loop)\
\
\
Here's the full class for a singly linked list in TypeScript:

```typescript
class Node {
  public next: Node | null;
  constructor(public val: any) {
    this.val = val;
    this.next = null;
  }
}

class SinglyLinkedList {
  length: number;
  head: Node | null;
  tail: Node | null;

  constructor() {
    this.length = 0;
    this.head = null;
    this.tail = null;
  }

  public push(val: any) {
    const node = new Node(val);

    if (!this.head) {
      this.head = node;
      this.tail = this.head;
      this.length = 1;
    } else {
      this.tail!.next = node;
      this.tail = node;
      this.length++;
    }
    return this;
  }

  public pop() {
    if (this.head == null) {
      return;
    }

    let current = this.head;
    let newTail = current;

    while (current.next != null) {
      newTail = current;
      current = current.next;
    }
    this.tail = newTail;
    this.tail.next = null;
    this.length--;

    if (this.length === 0) {
      this.head = null;
      this.tail = null;
    }

    return current;
  }

  public shift() {
    if (this.length === 0) return undefined;

    let current = this.head;

    this.head = current?.next!;
    this.length--;

    return current;
  }

  public unshift(val: any) {
    let newHead = new Node(val);
    if (!this.head) {
      this.head = newHead;
      this.tail = newHead;
    } else {
      newHead.next = this.head;
      this.head = newHead;
    }

    this.length++;
    return this;
  }

  public get(index: number) {
    if (index < 0 || index >= this.length) return null;
    let current = this.head;
    for (let i = 0; i < index; i++) {
      current = current?.next!;
    }
    return current;
  }

  public set(val: any, index: number) {
    let foundNode = this.get(index);
    if (foundNode) {
      foundNode.val = val;
      return true;
    }
    return false;
  }

  public insert(val: any, index: number) {
    if (index < 0 || index > this.length) return false;
    const newNode = new Node(val);
    newNode.val = val;
    if (index === this.length) {
      this.push(val);
      return true;
    }
    if (index === 0) {
      this.unshift(val);
      return true;
    }
    newNode.next = this.get(index);
    this.get(index - 1)!.next = newNode;
    this.length++;
    return true;
  }

  public remove(index: number) {
    if (index < 0 || index > this.length) return undefined;
    if (index === this.length - 1) return this.pop();
    if (index === 0) return this.shift();
    let prev = this.get(index - 1);
    let nodeToRemove = this.get(index);
    prev!.next = nodeToRemove!.next;
    this.length--;
    return nodeToRemove;
  }

  public reverse() {
    let node = this.head;
    this.head = this.tail;
    this.tail = node;
    let next: Node | null;
    let prev = null;

    for (let i = 0; i < this.length; i++) {
      next = node!.next;
      node!.next = prev;
      prev = node;
      node = next;
    }

    return this
  }
}

```
