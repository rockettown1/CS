---
description: Going through each item one at a time (searching by comparison)
---

# Linear Search

```javascript
//JavaScript

function linearSearch(arr, val){
    for (let i = 0; i < arr.length; i++){
        if (arr[i] === val){
            return true
        }
    }
    return false
}
```

### Big O&#x20;

Time Complexity:

| Best                    | Average | Worst                              |
| ----------------------- | ------- | ---------------------------------- |
| O(1)                    | O(n)    | O(n)                               |
| Find item straight away |         | Item at the end or not in the list |
