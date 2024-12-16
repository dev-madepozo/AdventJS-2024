# Challenge #15: ✏️ Drawing tables

#### Level: `🟢 EASY`

## Instructions

`ChatGPT has arrived at the North Pole` and the elf Sam Elfman is working on an application for managing gifts and children.

To enhance the presentation, he wants to create a function drawTable that receives an array of objects and converts it into a text table.

The drawn table should represent the object data as follows:

- It has a header with the column name.
- The column name has the `first letter capitalized`.
- Each row should contain the values of the objects in the corresponding order.
- Each value must be left-aligned.
- Fields always leave a space on the left.
- Fields leave the necessary space on the right to align the box.

Look at the example to see how you should draw the table:

**Examples:**

```js
drawTable([
  { name: 'Alice', city: 'London' },
  { name: 'Bob', city: 'Paris' },
  { name: 'Charlie', city: 'New York' }
])
// +---------+-----------+
// | Name    | City      |
// +---------+-----------+
// | Alice   | London    |
// | Bob     | Paris     |
// | Charlie | New York  |
// +---------+-----------+

drawTable([
  { gift: 'Doll', quantity: 10 },
  { gift: 'Book', quantity: 5 },
  { gift: 'Music CD', quantity: 1 }
])
// +----------+----------+
// | Gift     | Quantity |
// +----------+----------+
// | Doll     | 10       |
// | Book     | 5        |
// | Music CD | 1        |
// +----------+----------+
```

## Solutions

- **JavaScript**

  ```js
  /**
  * @param {Array<Object>} data
  * @returns {string}
  */
  function drawTable(data) {
    const colWidth = {}

    for (const row of data) {
      for (const [k, v] of Object.entries(row)) {
        colWidth[k] = Math.max(~~colWidth[k], k.length + 2, `${v}`.length + 2)
      }
    }

    let border = '+'
    for (const k in colWidth)
      border += '-'.repeat(colWidth[k]) + '+'

    let header = '|'
    for (const k in colWidth) {
      const [a, ...abc] = k
      header += ` ${a.toUpperCase()}${abc.join('')}`.padEnd(colWidth[k]) + '|'
    }

    const body = data.map(row => 
      `|${Object.keys(colWidth).map(k => ` ${row[k]}`.padEnd(colWidth[k])).join('|')}|`
    )

    return [border, header, border, ...body, border].join('\n')
  }
  ```

- **TypeScript**

  ```ts
  function drawTable(data: Array<Record<string, string | number>>): string {
    const colWidth = {}

    for (const row of data) {
      for (const [k, v] of Object.entries(row)) {
        colWidth[k] = Math.max(~~colWidth[k], k.length + 2, `${v}`.length + 2)
      }
    }

    let border = '+'
    for (const k in colWidth)
      border += '-'.repeat(colWidth[k]) + '+'

    let header = '|'
    for (const k in colWidth) {
      const [a, ...abc] = k
      header += ` ${a.toUpperCase()}${abc.join('')}`.padEnd(colWidth[k]) + '|'
    }

    const body = data.map(row => 
      `|${Object.keys(colWidth).map(k => ` ${row[k]}`.padEnd(colWidth[k])).join('|')}|`
    )

    return [border, header, border, ...body, border].join('\n')
  }
  ```

- **Python**

  ```py
  ```
