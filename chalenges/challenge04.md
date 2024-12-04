# Challenge #4: 🎄 Decorating the Christmas tree

#### Level: `🟠 MEDIUM`

## Instructions

`It's time to put up the Christmas tree at home!` 🎄 But this year we want it to be special. We're going to create a function that receives the height of the tree (a positive integer between 1 and 100) and a special character to decorate it.

The function should return a string that represents the Christmas tree, constructed as follows:

- The tree is made up of triangles of special characters.
- The spaces on the sides of the tree are represented with underscores _.
- All trees have a trunk of two lines, represented by the # character.
- The tree should always have the same length on each side.
- You must ensure the tree has the correct shape using line breaks \n for each line.

**Examples:**

```js
const tree = createXmasTree(5, '*')
console.log(tree)
/*
____*____
___***___
__*****__
_*******_
*********
____#____
____#____
*/

const tree2 = createXmasTree(3, '+')
console.log(tree2)
/*
__+__
_+++_
+++++
__#__
__#__
*/

const tree3 = createXmasTree(6, '@')
console.log(tree3)
/*
_____@_____
____@@@____
___@@@@@___
__@@@@@@@__
_@@@@@@@@@_
@@@@@@@@@@@
_____#_____
_____#_____
*/
```

## Solutions

- **JavaScript**

  ```js
  function createXmasTree(height, ornament) {
    let xmasTree = ''
    const spaces = '_'.repeat(height - 1)

    for (let i = 1; i <= height; i++) {
      const spaces = '_'.repeat(height - i)
      const ornaments = ornament.repeat(i * 2 - 1)
      xmasTree += `${spaces}${ornaments}${spaces}\n`
    }

    xmasTree += `${spaces}#${spaces}\n${spaces}#${spaces}`

    return xmasTree
  }
  ```

- **TypeScript**

  ```ts
  function createXmasTree(height: number, ornament: string): string {
    let xmasTree: string = ''
    const spaces: string = '_'.repeat(height - 1)

    for (let i = 1; i <= height; i++) {
      const spaces: string = '_'.repeat(height - i)
      const ornaments: string = ornament.repeat(i * 2 - 1)
      xmasTree += `${spaces}${ornaments}${spaces}\n`
    }

    xmasTree += `${spaces}#${spaces}\n${spaces}#${spaces}`

    return xmasTree
  }
  ```
- **Python**

  ```py
  def createXmasTree(height, ornament):
    xmas_tree = ""
    trunk_spaces = '_' * height - 1

    for i in range(1, height + 1):
      spaces = '_' * height - i
      ornaments = ornament * (i * 2 - 1)
      xmas_tree += spaces + ornaments + spaces + '\n'
    
    xmas_tree += trunk_spaces + '#' + trunk_spaces + '\n'
    xmas_tree += trunk_spaces + '#' + trunk_spaces

    return xmas_tree
  ```
