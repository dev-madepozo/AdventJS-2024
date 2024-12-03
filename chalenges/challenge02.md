# Challenge #2: 🖼️ Framing names

#### Level: `🟢 EASY`

## Instructions

Santa Claus 🎅 wants to frame the names of the good children to decorate his workshop 🖼️, but the frame must follow specific rules. Your task is to help the elves generate this magical frame.

Rules:

- Given an array of names, you must create a rectangular frame that contains all of them.
- Each name must be on a line, aligned to the left.
- The frame is built with * and has a border one line thick.
- The width of the frame automatically adapts to the longest name plus a margin of 1 space on each side.
Example of how it works:

```js
createFrame(['midu', 'madeval', 'educalvolpz'])

// Expected result:
***************
* midu        *
* madeval     *
* educalvolpz *
***************

createFrame(['midu'])

// Expected result:
********
* midu *
********

createFrame(['a', 'bb', 'ccc'])

// Expected result:
*******
* a   *
* bb  *
* ccc *
*******

createFrame(['a', 'bb', 'ccc', 'dddd'])
```

## Solutions

- **JavaScript**

  ```js
  function createFrame(names) {
    const largestNameSize = Math.max(...names.map(name => name.length))
    const border = '*'.repeat(largestNameSize + 4)
    const framedNames = names.map(name => `* ${name.padEnd(largestNameSize)} *`)

    return [border, ...framedNames, border].join('\n')
  }
  ```

- **TypeScript**

  ```js
  function createFrame(names: string[]): string {
    const largestNameSize: number = Math.max(...names.map(name => name.length))
    const border: string = '*'.repeat(largestNameSize + 4)
    const framedNames: string[] = names.map((name: string) => 
      `* ${name.padEnd(largestNameSize)} *`
    )

    return [border, ...framedNames, border].join('\n')
  }
  ```
- **Python**

  ```python
  def createFrame(names):
    largest_name_size = len(max(names, key=len))
    border = '*' * (largest_name_size + 4)
    framed_names = [f"* {name.ljust(largest_name_size)} *" for name in names]

    return '\n'.join([border] + framed_names + [border])
  ```