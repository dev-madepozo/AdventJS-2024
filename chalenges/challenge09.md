# Challenge #9: 🚂 The magic train

#### Level: `🟠 MEDIUM`

## Instructions

The elves are playing with a `magical train 🚂 that carries gifts`. This train moves on a board represented by an `array of strings`.

The train consists of an engine (@), followed by its carriages (o), and must collect magical fruits (*) which serve as fuel. The movement of the train follows these rules:

You will receive two parameters board and mov.

`board` is an array of strings that represents the board:

- @ is the train's engine.
- o are the train's carriages.
- \* is a magical fruit.
- · are empty spaces.

`mov` is a string that indicates the next movement of the train from the train's head @:

- 'L': left
- 'R': right
- 'U': up
- 'D': down.

With this information, you must return a string:

- 'crash': If the train crashes into the edges of the board or itself.
- 'eat': If the train collects a magical fruit (*).
- 'none': If it moves without crashing or collecting any magical fruit.

**Examples:**

```js
const board = ['·····', '*····', '@····', 'o····', 'o····']

console.log(moveTrain(board, 'U'))
// ➞ 'eat'
// Because the train moves up and finds a magical fruit

console.log(moveTrain(board, 'D'))
// ➞ 'crash'
// The train moves down and the head crashes into itself

console.log(moveTrain(board, 'L'))
// ➞ 'crash'
// The train moves to the left and crashes into the wall

console.log(moveTrain(board, 'R'))
// ➞ 'none'
// The train moves to the right and there is empty space on the right
```

## Solutions

- **JavaScript**

  ```js
  function moveTrain(board, mov) {
    const x = board.findIndex(row => row.includes('@'))
    const y = board[x].indexOf('@')

    const result = {'*': 'eat', '·': 'none', 'o': 'crash', undefined: 'crash'}
    const moves = {U: [x - 1, y], D: [x + 1, y], L: [x, y - 1], R: [x, y + 1]}
    const [dx, dy] = moves[mov]

    return result[board[dx]?.[dy]]
  }
  ```

- **TypeScript**

  ```ts
  type Space = '·' | '@' | '*' | 'o'
  type Board = Space[]
  type Movement = 'U' | 'D' | 'R' | 'L'
  type Result = 'none' | 'crash' | 'eat'

  function moveTrain(board: Board, mov: Movement): Result {
    const x: number = board.findIndex((row: string) => row.includes('@'))
    const y: number = board[x].indexOf('@')
    const result = {'*': 'eat', '·': 'none', 'o': 'crash', undefined: 'crash'}
    const moves = {U: [x - 1, y], D: [x + 1, y], L: [x, y - 1], R: [x, y + 1]}
    const [dx, dy] = moves[mov]
    return result[board[dx]?.[dy]]
  }
  ```

- **Python**

  ```py
  from typing import List, Literal

  def move_train(board: List[str], mov: Literal['U', 'D', 'R', 'L']) -> Literal['none', 'crash', 'eat']:
    x = next(i for i, row in enumerate(board) if '@' in row)
    y = board[x].index('@')

    moves = {
      'U': (x - 1, y),
      'D': (x + 1, y),
      'R': (x, y + 1),
      'L': (x, y - 1)
    }
    result = {
      '*': 'eat',
      '·': 'none',
      'o': 'crash'
    }

    new_x, new_y = moves[mov]

    try:
      return result[board[new_x][new_y]]
    except IndexError:
      return 'crash'
  ```
