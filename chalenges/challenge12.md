# Challenge #12: 💵 How much does the tree cost?

#### Level: `🟢 EASY`

## Instructions

You are in a very special market where Christmas trees 🎄 are sold. Each one comes decorated with a series of very peculiar ornaments, and the price of the tree is determined by the ornaments it has.

- `*`: Snowflake - Value: 1
- `o`: Christmas Ball - Value: 5
- `^`: Decorative Tree - Value: 10
- `#`: Shiny Garland - Value: 50
- `@`: Polar Star - Value: 100

Normally, you would sum up all the values of the ornaments and that's it…

But, watch out! `If an ornament is immediately to the left of another of greater value, instead of adding, its value is subtracted.`

**Examples:**

```js
calculatePrice('***')  // 3   (1 + 1 + 1)
calculatePrice('*o')   // 4   (5 - 1)
calculatePrice('o*')   // 6   (5 + 1)
calculatePrice('*o*')  // 5  (-1 + 5 + 1) 
calculatePrice('**o*') // 6  (1 - 1 + 5 + 1) 
calculatePrice('o***') // 8   (5 + 3)
calculatePrice('*o@')  // 94  (-5 - 1 + 100)
calculatePrice('*#')   // 49  (-1 + 50)
calculatePrice('@@@')  // 300 (100 + 100 + 100)
calculatePrice('#@')   // 50  (-50 + 100)
calculatePrice('#@Z')  // undefined (Z is unknown)
```

## Solutions

- **JavaScript**

  ```js
  /** @param {string} ornaments
   * @return {number | undefined} - The price of the tree
  */
  function calculatePrice(ornaments) {
    const costs = {'*': 1, 'o': 5, '^': 10, '#': 50, '@': 100}

    return [...ornaments].reduce((acc, cur, i, arr) => (
      acc + ([1, -1].at(costs[cur] < costs[arr[++i]])) * costs[cur]
    ), 0) || undefined
  }
  ```

- **TypeScript**

  ```ts
  /** @param {string} ornaments
   * @return {number | undefined} - The price of the tree
  */
  function calculatePrice(ornaments: string): number | undefined {
    const costs = {'*': 1, 'o': 5, '^': 10, '#': 50, '@': 100}

    return [...ornaments].reduce((acc, cur, i, arr) => (
      acc + ([1, -1].at(costs[cur] < costs[arr[++i]])) * costs[cur]
    ), 0) || undefined
  }
  ```

- **Python**

  ```py
  def calculate_price(ornaments):
    costs = {'*': 1, 'o': 5, '^': 10, '#': 50, '@': 100}

    tree_price = 0
    for i in range(len(ornaments)):
      current_cost = costs[ornaments[i]]
      if i + 1 < len(ornaments) and costs[ornaments[i]] < costs[ornaments[i + 1]]:
          total_price -= current_cost
      else:
          total_price += current_cost

    return total_price || undefined
  ```
