# Challenge #16: ❄️ Cleaning the snow path

#### Level: `🟢 EASY`

## Instructions

The elves are working hard to clear paths filled with magical snow ❄️. This snow has a special property: if two `identical and adjacent` snow piles are found, they `disappear automatically`.

Your task is to write a function to help the elves simulate this process. `The path is represented by a string and each snow pile by a character.`

You need to remove all adjacent snow piles that are the same `until no more moves are possible.`

The result should be the final path after removing all duplicate piles:

**Examples:**

```js
removeSnow('zxxzoz') // -> "oz"
// 1. Remove "xx", resulting in "zzoz"
// 2. Remove "zz", resulting in "oz"

removeSnow('abcdd') // -> "abc"
// 1. Remove "dd", resulting in "abc"

removeSnow('zzz') // -> "z"
// 1. Remove "zz", resulting in "z"

removeSnow('a') // -> "a"
// No duplicate piles
```

## Solutions

- **JavaScript**

  ```js
  /**
  * @param {string} s
  * @returns {string}
  */
  function removeSnow(s) {
    let clear = ''
    for (const c of s)
      clear = [clear + c, clear.slice(0, -1)][+(clear.endsWith(c))]
    return clear;
  }
  ```

- **TypeScript**

  ```ts
  /**
   * @param {string} s
  * @returns {string}
  */
  function removeSnow(s: string): string {
    let clear = ''
    for (const c of s)
      clear = [clear + c, clear.slice(0, -1)][+(clear.endsWith(c))]
    return clear;
  }
  ```

- **Python**

  ```py
  def remove_snow(s):
    clear = ''
    for c in s:
        clear = [clear + c, clear[:-1]][int(clear.endswith(c))]
    return clear
  ```
