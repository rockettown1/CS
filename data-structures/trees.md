---
description: >-
  Trees are non-linear, there are many paths/branches you can take. There is a
  parent - child relationship, where each node can only point to nodes below it
  in the tree.
---

# Trees

Here's a random example of what a tree structure might look like

<img src="../.gitbook/assets/file.drawing (3).svg" alt="" class="gitbook-drawing">

Terminology:

* Root - The top node in a tree
* Child - A node directly connected to another node when moving away from the parent.
* Parent - The converse notion of a child
* Siblings - A group of nodes with the same parent.
* Leaf - A node with no children
* Edge - The connection between one node and another

Common use cases:

* The DOM
* React.js component tree
* Network routing
* Abstract syntax tree (how code is parsed)
* AI and machine learning
* Folders in an operating system

### Binary Trees

With a binary tree, each node can have (at most) two children.

#### Binary Search Trees (aka Ordered Binary Tree aka Sorted Binary Tree)

BSTs store ordered data, where every item less than the parent is to the left, and every item greater than the parent is to the right.

<img src="../.gitbook/assets/file.drawing (1).svg" alt="" class="gitbook-drawing">

Here's an implementation in TypeScript. Note that each item in the tree is represented as a Node (just like a linked list)

```typescript
class Node {
  left: Node | null;
  right: Node | null;
  val: number;

  constructor(val: number) {
    this.val = val;
    this.left = null;
    this.right = null;
  }

```

And the Binary Search Tree itself only has one property, the root.

```typescript
class BinarySearchTree {
  root: Node | null;
  constructor() {
    this.root = null;
  }
}
```

We of course need to be able to insert Nodes into this tree, and we determine its position by comparing it to the current value, starting at the root and deciding whether to go left and right. If we find a Node were the left or right doesn't already exist, we insert it.

NOTE on handling duplicates:\
Depending on your use case, you may just want to ignore duplicates. In this implementation I have modified my Node class to include a frequency field to keep track of how many times that number has been inserted into the tree. Feel free to ignore this.

```typescript
class Node {
  left: Node | null;
  right: Node | null;
  val: number;
  frequency: number;

  constructor(val: number) {
    this.val = val;
    this.frequency = 1;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree {
  root: Node | null;
  constructor() {
    this.root = null;
  }

  public insert(val: number) {
    const newNode = new Node(val);
    let current = this.root;
    
    //if there's no root, make the newNode the root
    if (!current) {
      this.root = newNode;
      return this;
    }

    /* 
       We want to keep looping until we find a place for it, but must remember to
       return at the correct points to break the infinite loop.
       We start with the current equal to the root, and compare to the value being
       inserted, once we decide left or right, we update current.
    */
   while (true) {
      if (val === current.val) {
        current.frequency++;
        return this;
      }
      if (val > current.val) {
        if (current.right) {
          current = current.right;
        } else {
          current.right = newNode;
          return this;
        }
      } else if (val < current.val) {
        if (current.left) {
          current = current.left;
        } else {
          current.left = newNode;
          return this;
        }
      }
    }
  }
}
```

Searching for a value is very similar to inserting. When we were inserting, if we found a place where the left or right didn't exist, we inserted the value in the correct place.&#x20;

While searching, we follow the same steps but instead of inserting we return false because the value we were looking for isn't in there (we hit a dead end in the tree)

```typescript
public search(val: number) {
    let current = this.root;

    if (!current) {
      return false;
    }

    while (true) {
      if (val == current.val) {
        return true;
      }

      if (val > current.val) {
        if (current.right) {
          current = current.right;
        } else {
          return false;
        }
      } else if (val < current.val) {
        if (current.left) {
          current = current.left;
        } else {
          return false;
        }
      }
    }
  }
```

Notes on traversing trees can be found in the sections on [Breadth First Search](../searching-algorithms/breadth-first-search.md) and [Depth First Search](../searching-algorithms/depth-first-search.md), in the searching-algorithm part of this book.
