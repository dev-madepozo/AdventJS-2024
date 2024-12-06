# Challenge #6: 📦 Is the gift inside the box?

#### Level: `🟠 MEDIUM`

## Instructions

We have already wrapped hundreds of presents 🎁… but an elf forgot to check if the present, represented by an asterisk *, is inside the box.

The box has a present (*) and counts as "inside the box" if:

- It is completely surrounded by # on the box's edges.
- The * is not on the box's edges.

Keep in mind that the * can be inside, outside, or may not even be there. We must return true if the * is inside the box and false otherwise.

**Examples:**

```js
inBox([
  "###",
  "#*#",
  "###"
]) // ➞ true

inBox([
  "####",
  "#* #",
  "#  #",
  "####"
]) // ➞ true

inBox([
  "*####",
  "#   #",
  "#  #*",
  "####"
]) // ➞ false

inBox([
  "#####",
  "#   #",
  "#   #",
  "#   #",
  "#####"
]) // ➞ false
```

## Solutions

- **JavaScript**

  ```js
  function inBox(box) {
    return box.slice(1, -1).some(line => /^# *\* *#$/.test(line))
  }
  ```

- **TypeScript**

  ```ts
  function inBox(box: string[]): boolean {
    return box.slice(1, -1).some(
      (line: string) => /^# *\* *#$/.test(line)
    )
  }
  ```

- **Python**

  ```py
  import re

  def inBox(box):
    return any(re.match(r'^# *\* *#$', line) for line in box[1:-1])
  ```
