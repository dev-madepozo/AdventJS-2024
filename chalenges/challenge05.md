# Challenge #5: 👞 Shoe pairing

#### Level: `🟢 EASY`

## Instructions

`Santa Claus's elves` 🧝🧝‍♂️ have found a bunch of mismatched magic boots in the workshop. Each boot is described by two values:

- type indicates if it's a left boot (I) or a right boot (R).
- size indicates the size of the boot.

Your task is to help the elves pair all the boots of the same size having a left and a right one. To do this, you should return a list of the available sizes after pairing the boots.

**Examples:**

```js
const shoes = [
  { type: 'I', size: 38 },
  { type: 'R', size: 38 },
  { type: 'R', size: 42 },
  { type: 'I', size: 41 },
  { type: 'I', size: 42 }
]

organizeShoes(shoes)
// [38, 42]

const shoes2 = [
  { type: 'I', size: 38 },
  { type: 'R', size: 38 },
  { type: 'I', size: 38 },
  { type: 'I', size: 38 },
  { type: 'R', size: 38 }
]
// [38, 38]

const shoes3 = [
  { type: 'I', size: 38 },
  { type: 'R', size: 36 },
  { type: 'R', size: 42 },
  { type: 'I', size: 41 },
  { type: 'I', size: 42 }
]

organizeShoes(shoes3)
// [42]
```

## Solutions

- **JavaScript**

  ```js
  function organizeShoes(shoes) {
    const availableSizes = []
    const shoesBySize = {}

    for (const { size, type } of shoes) {
      shoesBySize[size] ??= { I: 0, R: 0 }
      shoesBySize[size][type]++

      if (shoesBySize[size].I && shoesBySize[size].R) {
        availableSizes.push(size)
        shoesBySize[size].I--
        shoesBySize[size].R--
      }
    }

    return availableSizes
  }
  ```

- **TypeScript**

  ```ts
  type Shoe = {
    type: 'I' | 'R'
    size: number
  }

  type ShoesBySize = {
    [key: number]: {
      I: number,
      R: number
    }
  }

  function organizeShoes(shoes: Shoe[]): number[] {
    const availableSizes: number[] = []
    const shoesBySize: ShoesBySize = {}

    for (const { size, type } of shoes) {
      shoesBySize[size] ??= { I: 0, R: 0 }
      shoesBySize[size][type]++

      if (shoesBySize[size].I && shoesBySize[size].R) {
        availableSizes.push(size)
        shoesBySize[size].I--
        shoesBySize[size].R--
      }
    }

    return availableSizes
  }
  ```

- **Python**

  ```py
  def organizeShoes(shoes):
    available_sizes = []
    shoes_by_size = {}

    for shoe in shoes:
      type_, size = shoe['type'], shoe['size']

      if size not in shoes_by_size:
        shoes_by_size[size] = { 'I': 0, 'R': 0 }

      shoes_by_size[size][type_] += 1

      if shoes_by_size[size]['I'] > 0 and shoes_by_size[size]['R'] > 0:
        available_sizes.append(size)
        shoes_by_size[size]['I'] -= 1
        shoes_by_size[size]['R'] -= 1

    return available_sizes
  ```
