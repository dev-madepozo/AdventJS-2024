# Challenge #13: 🤖 Is the robot back?

#### Level: `🟠 MEDIUM`

## Instructions

The North Pole elves have created a special robot 🤖 that helps Santa Claus distribute gifts inside a large warehouse. `The robot moves in a 2D plane starting from the origin (0, 0).`

We want to know if, after executing a series of movements, the robot ends up exactly where it started.

The robot's basic commands are:

- **L**: Move to the left
- **R**: Move to the right
- **U**: Move upwards
- **D**: Move downwards

But it also has certain movement modifiers:

- *: The movement is performed with double intensity (e.g., *R means RR)
- !: The next movement is inverted (e.g., R!L performs as RR)
- ?: The next movement is only executed if it hasn't been done before (e.g., R?R means R)

`Note`: Keep in mind that when the movement is inverted with !, the original movement is counted for ?. For example, !U?U inverts the movement of U but counts as if the U movement was performed.

You should return:

- true: if the robot ends up exactly where it started
- [x, y]: if the robot does not end up exactly where it started, return the position where it stopped

**Examples:**

```js
isRobotBack('R')     // [1, 0]
isRobotBack('RL')    // true
isRobotBack('RLUD')  // true
isRobotBack('*RU')   // [2, 1]
isRobotBack('R*U')   // [1, 2]
isRobotBack('LLL!R') // [-4, 0]
isRobotBack('R?R')   // [1, 0]
isRobotBack('U?D')   // true
isRobotBack('R!L')   // [2,0]
isRobotBack('U!D')   // [0,2]
isRobotBack('R?L')   // true
isRobotBack('U?U')   // [0,1]
isRobotBack('*U?U')  // [0,2]
isRobotBack('R!U?U') // [1,0]
isRobotBack('U?D?U') // true
```

## Solutions

- **JavaScript**

  ```js
  function isRobotBack(moves) {
    let x = 0, y = 0, i = 0
    const arr = [...moves]
    const direction = {
      'R': () => x += 1,
      'L': () => x -= 1,
      'D': () => y -= 1,
      'U': () => y += 1,
      '*': (nextMove) => direction[nextMove](),
      '!': (nextMove) => {
        if ('LR'.includes(nextMove)) {
          arr[i + 1] = ['L', 'R'][+(nextMove == 'L')]
        } else {
          arr[i + 1] = ['U', 'D'][+(nextMove == 'U')]
        }
      },
      '?': (nextMove) => arr.lastIndexOf(nextMove, i) > -1 ? arr[i + 1] = '' : null
    }

    while (i < arr.length) {
      const move = arr[i]
      move in direction && direction[move](moves[i + 1])
      i++
    }

    return [true, [x, y]][+!!(x + y)]
  }
  ```

- **TypeScript**

  ```ts
  function isRobotBack(moves: string[]): true | [number, number] {
    let x = 0, y = 0, i = 0
    const arr = [...moves]
    const direction = {
      'R': () => x += 1,
      'L': () => x -= 1,
      'D': () => y -= 1,
      'U': () => y += 1,
      '*': (nextMove) => direction[nextMove](),
      '!': (nextMove) => {
        if ('LR'.includes(nextMove)) {
          arr[i + 1] = ['L', 'R'][+(nextMove == 'L')]
        } else {
          arr[i + 1] = ['U', 'D'][+(nextMove == 'U')]
        }
      },
      '?': (nextMove) => arr.lastIndexOf(nextMove, i) > -1 ? arr[i + 1] = '' : null
    }

    while (i < arr.length) {
      const move = arr[i]
      move in direction && direction[move](moves[i + 1])
      i++
    }

    return [true, [x, y]][+!!(x + y)]
  }
  ```

- **Python**

  ```py
  ```
