# Challenge #13: 🤖 Is the robot back?

#### Level: `🔴 HARD`

## Instructions

The elves at the North Pole have created a special robot 🤖 that helps Santa Claus distribute gifts inside a large warehouse. `The robot moves on a 2D plane and we start from the origin (0, 0).`

We want to know if, after executing a series of movements, the robot returns to exactly where it started.

The robot's basic commands are:

- **L**: Move to the left
- **R**: Move to the right
- **U**: Move upwards
- **D**: Move downwards

But it also has certain modifiers for the movements:

- *: The movement is done with double intensity (e.g., *R means RR)
- !: The next movement is inverted (e.g., R!L is considered as RR)
- ?: The next movement is done only if it hasn't been done before (e.g., R?R means R)

**Note**: When the movement is inverted with ! `the inverted movement is counted and not the original one`. For example, !U?U inverts the U movement, so it counts as having done the D movement but not the U. Thus, !U?U translates to D?U, and therefore, the final U movement is done.

You should return:

- `true`: if the robot returns exactly to where it started
- [x, y]: if the robot does not return to where it started, return the position where it stopped

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
isRobotBack('U?D?U') // true

// Ejemplos paso a paso:
isRobotBack('R!U?U') // [1,0]
// 'R'  -> se mueve a la derecha 
// '!U' -> se invierte y se convierte en 'D'
// '?U' -> se mueve arriba, porque no se ha hecho el movimiento 'U'

isRobotBack('UU!U?D') // [0,1]
// 'U'  -> se mueve arriba
// 'U'  -> se mueve arriba
// '!U' -> se invierte y se convierte en 'D'
// '?D' -> no se mueve, ya que ya se hizo el movimiento 'D'
```

## Solutions

- **JavaScript**

  ```js
  function isRobotBack(moves) {
    let x = 0, y = 0
    const arr = [...moves]
    const operations = {
      'R': () => x += 1,
      'L': () => x -= 1,
      'D': () => y -= 1,
      'U': () => y += 1,
      '*': (next) => operations[next](),
      '!': (next, nextPos) =>
        'LR'.includes(next)
        ? arr[nextPos] = ['L', 'R'][+(next == 'L')]
        : arr[nextPos] = ['U', 'D'][+(next == 'U')],
      '?': (next, nextPos) => 
        arr[nextPos] = [next, ''].at(arr.lastIndexOf(next, nextPos - 1) > -1)
    }

    for (const i in arr)
      operations[arr[i]]?.(moves[+i + 1], +i + 1)

    return [true, [x, y]][+!!(x + y)]
  }
  ```

- **TypeScript**

  ```ts
  function isRobotBack(moves: string[]): true | [number, number] {
    let x = 0, y = 0
    const arr = [...moves]
    const operations = {
      'R': () => x += 1,
      'L': () => x -= 1,
      'D': () => y -= 1,
      'U': () => y += 1,
      '*': (next) => operations[next](),
      '!': (next, nextPos) =>
        'LR'.includes(next)
        ? arr[nextPos] = ['L', 'R'][+(next == 'L')]
        : arr[nextPos] = ['U', 'D'][+(next == 'U')],
      '?': (next, nextPos) => 
        arr[nextPos] = [next, ''].at(arr.lastIndexOf(next, nextPos - 1) > -1)
    }

    for (const i in arr)
      operations[arr[i]]?.(moves[+i + 1], +i + 1)

    return [true, [x, y]][+!!(x + y)]
  }
  ```

- **Python**

  ```py
  ```
