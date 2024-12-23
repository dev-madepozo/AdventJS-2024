# Challenge #23: 🔢 Find the missing numbers

#### Level: `🟢 EASY`

## Instructions

The elves are working on a system to verify children's gift lists 👧👦. However, some lists are incomplete and `numbers are missing!`

Your task is to write `a function that, given an array of numbers, finds all the numbers that are missing between 1 and n` (where n is the size of the array or the highest number in the array).

Keep in mind that:

- Numbers may appear more than once and others may be missing
- The array always contains positive integers
- Counting always starts from 1

**Examples:**

```js
findMissingNumbers([1, 2, 4, 6])
// [3, 5]

findMissingNumbers([4, 8, 7, 2])
// [1, 3, 5, 6]

findMissingNumbers([3, 2, 1, 1])
// []

findDisappearedNumbers([5, 5, 5, 3, 3, 2, 1])
// [4]
```

## Solutions

- **JavaScript**

  ```js
  /**
  * @param {number[]} nums - List of integers.
  * @returns {number[]} - List of missing numbers.
  */
  function findMissingNumbers(nums) {
    const length = Math.max(...nums)
    const fullList = Array.from({ length }).map((_, i) => ++i)
    return [...new Set(fullList).difference(new Set(nums))]
  }
  ```

- **TypeScript**

  ```ts
  /**
  * @param {number[]} nums - List of integers.
  * @returns {number[]} - List of missing numbers.
  */
  function findMissingNumbers(nums: number[]): number[] {
    const length = Math.max(...nums)
    const missingNumbers = []
    for (let i = 1; i < length; i++) {
      !nums.includes(i) && missingNumbers.push(i)
    }
    return missingNumbers
  }
  ```

- **Python**

  ```py
  def find_missing_numbers(nums):
    n = max(nums)
    return [x for x in range(1, n) if x not in nums]
  ```
