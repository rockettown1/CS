---
description: >-
  The order we visit nodes in a tree (visit nodes on the same level and work our
  way down the tree)
---

# Breadth First Search (BFS)

When we are working with a tree structure we are able to use the BFS algorithm. The implementation of the algorithm depends on what kind of tree we are searching through, in the examples here I'll show an implementation for working with a Binary Search Tree (ie where each node has a left and right property) but also a more generic implementation for working with a generic tree structure (ie where each node has a children property.

This algorithm makes use of a queue (check the [Stacks & Queues](../data-structures/stacks-and-queues.md#queues) section for a recap if needed)

Image we are working with the following tree:

<img src="../.gitbook/assets/file.drawing (2).svg" alt="" class="gitbook-drawing">

We visit the nodes along the horizontal (breadth first) each level at a time. So the order in which we visit the nodes will be: 5, 2, 7, 1, 3, 6, 9 (or looking at the colours above: the red (root) node, the blue notes then the orange nodes).

The way we can keep track of nodes we need to visit is by using a queue, and we also store the values we have visited. In this explanation we won't be 'searching' for something, but rather just visiting each node in order.

In English\
Note: This algorithm runs as long as there is something in the queue. For this example we will keep track (store) each node we have visited in an array.

* We start by pushing the root node into the queue. Queue: \[ 5 ] Visited: \[ ]
* We check whether there is anything in the queue, and if there is we pop it off and store it in the visited array. Queue: \[ ] Visited: \[ 5 ]
* We then check whether the current node has a node to its left, and if it does store it in the queue. And do the same for the right Queue: \[ 2, 7 ] Visited: \[ 5 ]
* The process then repeats: We check whether anything is in the queue (yes), and we pop it off and store it in visited Queue: \[ 7 ] Visited: \[ 5, 2 ]
* We then check whether the current node (2) has anything on its left and right, if it does, they join the queue. Queue: \[ 7, 1, 3 ] Visited: \[ 5, 2 ]
* The process then repeats which looks like this:\
  Queue: \[ 1, 3, 6, 9 ] Visited: \[ 5, 2, 7 ]\
  Queue: \[ 3, 6, 9 ] Visited: \[ 5, 2, 7, 1 ]\
  Queue: \[ 6, 9 ] Visited: \[ 5, 2, 7, 1, 3 ]\
  Queue: \[ 9 ] Visited: \[ 5, 2, 7, 1, 3, 6 ]\
  Queue: \[  ] Visited: \[ 5, 2, 7, 1, 3, 6, 9 ]
* Nothing left in the queue so the algorithm has visited each node in order.

In an actual use case you might be searching for a value, in which case you would carry out a comparison against each node and stop if you find what you're looking for.&#x20;

Here's a code implementation of the above explanation in TypeScript. A few notes: It uses the Binary Search Tree class used in that section, in which each node has a left, right and value property. Also, for simplicity I shall use a basic array as the queue, but as mentioned in the Queue notes, we should really be implementing a queue using a linked list.

```typescript
//This function assumes we are using the BinarySearchTree class and Node class
//Go to that section to see the implementation

function BFS(bst: BinarySearchTree){
    let node = bst.root
    let visited: Node[] = []
    let queue: Node[] = []

    queue.push(node)

    while (queue.length > 0) {
        node = queue.shift()
        visited.push(node)
        if (node.left) queue.push(node.left)
        if (node.right) queue.push(node.right)
    }

return visited

}
```

### BFS on a generic tree structure

Below is a general example of the BFS algorithm on a tree (not specifically a binary tree). The tree in this example uses Nodes with the following structure for simplicity, but in reality it would of course have a value property. You can assume the Generic Tree class has a root property, the same as a Binary Tree.

```typescript
//generic Node class

class Node<T> {
  id: T;
  parentId: T | null;
  children?: Node<T>[] | null;

  constructor(id: T, parentId: T | null) {
    this.id = id;
    this.parentId = parentId;
    this.children = [];
  }
}
```

This example also uses a [custom Queue implementation](../data-structures/stacks-and-queues.md#queues) based on a linked list, with an enqueue and dequeue method. See that section for a reminder if needed.

```typescript
//Assumes we are using a GenericTree class
//See the appendix below for an implementation

function BFS(gt: GenericTree){
  const queue = new Queue();
  let visited = [];

  queue.enqueue(gt.root);

  while (queue.size > 0) {
    const dequeuedVal = queue.dequeue()!.val;
    visited.push(dequeuedVal.id);
    
    //queuing the children Nodes
    if (dequeuedVal.children.length > 0) {
      for (let child of dequeuedVal.children) {
        queue.enqueue(child);
      }
    }
  }

return visited;  
}
```

### Appendix

Here's a just for clarity implementation and population of a generic tree. Note: I've just made this up, I'm not claiming this is a good way of doing it. It's just if you wanted to copy the code into an editor and mess around with it:\


```typescript
class Node<T> {
  id: T;
  parentId: T | null;
  children?: Node<T>[] | null;

  constructor(id: T, parentId: T | null) {
    this.id = id;
    this.parentId = parentId;
    this.children = [];
  }
}

export class GenericTree<T> {
  root: Node<T> | null;

  constructor() {
    this.root = null;
  }

  public build(data: { id: T; parentId: T | null }[]) {
    let nodeArray: Node<T>[] = [];

    for (let i = 0; i < data.length; i++) {
      nodeArray.push(new Node<T>(data[i].id, data[i].parentId));
    }

    for (let i = 0; i < nodeArray.length; i++) {
      for (let j = 0; j < nodeArray.length; j++) {
        if (nodeArray[i].parentId == nodeArray[j].id) {
          nodeArray[j].children?.push(nodeArray[i]);
        }
      }
      if (!nodeArray[i].parentId) {
        this.root = nodeArray[i];
      }
    }
    return this;
  }
  
  public breathFirstSearch(){
    const queue = new Queue();
    let visited = [];

    queue.enqueue(this.root);

    while (queue.size > 0) {
      const dequeuedVal = queue.dequeue()!.val;
      
      //just using the id here for clarity
      visited.push(dequeuedVal.id);
    
      //queuing the children Nodes
      if (dequeuedVal.children.length > 0) {
        for (let child of dequeuedVal.children) {
          queue.enqueue(child);
        }
      }
    }

  return visited;  
  }
}



//convert this data into a generic tree structure
const data = [
  { id: 56, parentId: 62 },
  { id: 81, parentId: 80 },
  { id: 74, parentId: null },
  { id: 76, parentId: 80 },
  { id: 63, parentId: 62 },
  { id: 80, parentId: 86 },
  { id: 87, parentId: 86 },
  { id: 62, parentId: 74 },
  { id: 86, parentId: 74 },
];

const genTree = new GenericTree<number>().build(data);

const visitOrder = genTree.breathFirstSearch() 
// logs -> [74, 62, 86, 56, 63, 80, 87, 81, 76]

```

If we had the data from the diagram above:

```typescript
const data = [
  { id: 2, parentId: 5 },
  { id: 1, parentId: 2 },
  { id: 5, parentId: null },
  { id: 3, parentId: 2 },
  { id: 9, parentId: 7 },
  { id: 7, parentId: 5 },
  { id: 6, parentId: 7 }
]

const genTree = new GenericTree<number>().build(data);

const visitOrder = genTree.breathFirstSearch() 
// logs -> [5, 2, 7, 1, 4, 6, 9] as seen earlier
```
