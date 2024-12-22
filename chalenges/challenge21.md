# Challenge #21: 🎄 Calculate the height of the Christmas tree

#### Level: `🟢 EASY`

## Instructions

Santa Claus 🎅 is decorating a magical Christmas tree 🪄, which this year has a special structure in the form of a `binary tree`. Each node of the tree represents a gift, and Santa wants to know the height of the tree to place the magical star at the top.

Your task is to write a function that calculates the height of a binary tree. The height of a binary tree is defined as the maximum number of levels from the root to a leaf. An empty tree has a height of `0`.


**Examples:**

```js
// Tree definition
const tree = {
  value: '🎁',
  left: {
    value: '🎄',
    left: {
      value: '⭐',
      left: null,
      right: null
    },
    right: {
      value: '🎅',
      left: null,
      right: null
    }
  },
  right: {
    value: '❄️',
    left: null,
    right: {
      value: '🦌',
      left: null,
      right: null
    }
  }
}

// Graphical representation of the tree:
//        🎁
//       /   \
//     🎄     ❄️
//    /  \      \
//  ⭐   🎅      🦌

// Function call
treeHeight(tree)
// Returns: 3
```

## Solutions

- **JavaScript**

  ```js
  function treeHeight(tree) {
    if (!tree) return 0
    return Math.max(treeHeight(tree.left), treeHeight(tree.right)) + 1
  }
  ```

- **TypeScript**

  ```ts
  function treeHeight(tree: { value: string; left: any; right: any } | null): number {
    if (!tree) return 0
    return Math.max(treeHeight(tree.left), treeHeight(tree.right)) + 1
  }
  ```

- **Python**

  ```py
  def tree_height(tree):
    if tree is None:
      return 0
    return max(tree_height(tree.left), tree_height(tree.right)) + 1
  ```
