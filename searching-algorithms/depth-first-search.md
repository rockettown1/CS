---
description: >-
  The order we visit the nodes in a tree (we visit down each branch to the end
  of the tree before visiting sibling nodes)
---

# Depth First Search (DFS)

There are three main 'flavours' of DFS:

* Pre-order
* Post-order
* In-order

Imagine we have the following tree:

<img src="../.gitbook/assets/file.drawing (3).svg" alt="" class="gitbook-drawing">

### Pre Order

In Pre-order DFS we will visit the nodes in the following order - \[5, 2, 1, 3, 7, 6, 9]

Pre-order means we visit a node (first) then we check children nodes. So in the binary tree example, we would visit a node then look at the left and look at the right. Then choose to go left of right and repeat the process. Visit the node and check left and right. Once we hit the bottom of the tree, we will check sibling nodes in the same manner. (A very unclear explanation, so lets see a step by step example)

In English:\
With pre order we visit a node before looking whats next.\
We start with the root node (as always) then look at what's next: visited = \[5]\
In this example we'll go <mark style="color:red;">left first</mark>: visited = \[5, 2]\
And again: \[5, 2, 1]\
And then there are no more down after the 1 node.\
We then visit right of 2: visited = \[5, 2, 1, 3 ]\
No more after 3, so we visit to the right of the root and repeat the process:\
visited = \[5, 2, 1, 3, 7 ]\
visited = \[5, 2, 1, 3, 7, 6 ]\
visited = \[5, 2, 1, 3, 7, 6, 9 ]\
Done: We visited all the node "Depth first"

The tricky bit here is that we need to go back to revisit past nodes to see if there was a 'different path'. Although it seems that way, we can make use of a few programming concepts to help us do this. In this example I'll write the code both Recursively and Iteratively.

### DFS Preorder (recursive)

Here's we make use of a helper function (which I've called store, but can't remember why) which we will call recursively on each left and right node. The main job of this helper function is to push the node's value to the visited array, then check if there's anything left and repeat, then check if there's anything right and repeat. As always, it can be a little tricky to visualise the recursive calls so let's visualise it below.

```typescript
function dfsPreorder() {
    const visited: number[] = [];
    let current = this.root;

    if (!current) {
      return;
    }

    function store(node: Node) {
      visited.push(node.val);
      if (node.left) {
        store(node.left);
      }
      if (node.right) {
        store(node.right);
      }
    }

    store(current);

    return visited;
  }
```

So we start with the root and pass that to our helper function:\
\
**First call**\
first the root's value (Node 5) is pushed to the visited array: visited = \[5]\
\
**Second call (left side)**\
Then it's called recursively on Node 2: visited = \[5, 2]\
\
**Third call (left side and right side)**\
Then it's called on Node 1: visited = \[5, 2, 1]\
There's nothing more on the left or right, so we go back to the Second call\
\
**Second call (right side)**\
****We're back to the call on Node 2 where we call the function again on the right:\
\
**Fourth call (left and right side)**\
****Called on Node 3: visited = \[5, 2, 1, 3]\
There's nothing more on the left or right so we're go back to the Second call.\
\
**Second call (again)**\
****We've now gone down all the paths here so this function ends and goes back into the First call\
\
**First call** **(right side)**\
This time we go down the right side\
\
**Fifth call**\
****Called on Node 7: visited = \[5, 2, 1, 3, 7]\
\
**Sixth call (left and right side)**\
****Called on Node 6: visited = \[5, 2, 1, 3, 7, 6] \
There's nothing more on the left t so we go back to the Fifth call\
\
**Seventh call (left and right side)**\
****Called on Node 9: visited =  \[5, 2, 1, 3, 7, 6, 9]\
There's no more on the left and right so we go back to the Fifth call\
\
**Fifth call (again)**\
****We've now gone down all the paths so the function ends and we go back to the First call\
\
**First call (back for the final time)**\
We've not gone down all the paths so the function ends, and we go back to the main dfs function:\
\
And we then return the visited array. PHEW!



### DFS Preorder (Iterative)

In the iterative version of this algorithm we make use of a stack (last in first out) in a similar way to how breadth first search used a queue. The stack allows us to keep track of which nodes we've passed but not visited all the way. In this implementation (for simplicity) I'm going to use a standard JS array as the stack, but ideally we'd use our own stack implementation as well (linked list). We will keep looping until the stack is empty.

```typescript
function dfsPreorder(){
    const visited: number[] = [];
    const stack: Node[] = [];
    let node = this.root;
    
    if (node) {
      stack.push(node);
      while (stack.length > 0) {
        node = stack.pop() as Node; //we are certain it's not null here
        visited.push(node.val);
        
        if (node.right) {
          stack.push(node.right);
        }

        if (node.left) {
          stack.push(node.left);
        }
      }
    }
    return visited;
  }

}
```
