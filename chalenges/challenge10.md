# Challenge #10: 👩‍💻 The elfish assembler

#### Level: `🟠 MEDIUM`

## Instructions

The elf programmers are creating a `small magical assembler` to control the machines in Santa Claus's workshop.

To assist them, we will implement a simple interpreter that supports the following magical instructions:

- `MOV` x y: Copies the value x (which can be a number or the content of a register) into register y
- `INC` x: Increments the content of register x by 1
- `DEC` x: Decrements the content of register x by 1
- `JMP` x y: If the value in register x is 0, then jumps to the instruction at index y and continues executing the program from there.

Expected behavior:

- If an attempt is made to access, increment, or decrement a register that has not been initialized, the default value 0 will be used.
- The jump with `JMP` is absolute and goes to the exact index indicated by y.
- Upon completion, the program should return the content of register A. If A did not have a defined value, it returns undefined.

**Examples:**

```js
const instructions = [
  'MOV -1 C', // copies -1 to register 'C',
  'INC C', // increments the value of register 'C'
  'JMP C 1', // jumps to the instruction at index 1 if 'C' is 0
  'MOV C A', // copies register 'C' to register 'A',
  'INC A' // increments the value of register 'A'
]

compile(instructions) // -> 2

/**
 Step-by-step execution:
 0: MOV -1 C -> The register C receives the value -1
 1: INC C    -> The register C becomes 0
 2: JMP C 1  -> C is 0, jumps to the instruction at index 1
 1: INC C    -> The register C becomes 1
 2: JMP C 1  -> C is 1, the instruction is ignored
 3: MOV C A  -> Copies register C to A. Now A is 1
 4: INC A    -> The register A becomes 2
 */
```

> Note: Registers that have not been previously initialized are initialized to 0.

## Solutions

- **JavaScript**

  ```js
  function compile(instructions) {
    let i = 0
    const registers = {}
    const operations = {
      MOV: (x, y) => registers[y] = registers[x] || parseInt(x),
      INC: x => registers[x] += 1,
      DEC: x => registers[x] -= 1,
      JMP: (x, y) => !registers[x] && (i = y - 1)
    }

    while (i < instructions.length) {
      const [instruction, x, y] = instructions[i].split(' ')
      registers[x] ??= 0
      operations[instruction](x, y)
      i++
    }

    return registers.A
  }
  ```

- **TypeScript**

  ```ts
  /**
   * @param {string[]} instructions - The instructions to execute
  * @returns {number} The value of the register A
  */

  function compile (instructions: string[]): number {
    let i: number = 0
    const registers = {}
    const operations = {
      MOV: (x: string, y: string) => registers[y] = registers[x] || parseInt(x),
      INC: (x: string) => registers[x] += 1,
      DEC: (x: string) => registers[x] -= 1,
      JMP: (x: string, y: string) => !registers[x] && (i = y - 1)
    }

    while (i < instructions.length) {
      const [instruction, x, y] = instructions[i].split(' ')
      registers[x] ??= 0
      operations[instruction](x, y)
      i++
    }

    return registers['A']
  }
  ```

- **Python**

  ```py
  def compile(instructions):
    i = 0
    registers = {}
    operations = {
      'MOV': lambda x, y: registers[y] = registers.get(x, 0) if x in registers else int(x),
      'INC': lambda x: registers[x] = registers.get(x, 0) + 1
      'DEC': lambda x: registers[x] = registers.get(x, 0) - 1
      'JMP': lambda x, y: i = int(y) - 1 if not registers.get(x, 0)
    }

    while i < len(instructions):
      instruction, x, y = instructions[i].split()
      registers.setdefault(x, 0)
      operations[instruction](x, y)
      i += 1

    return registers.get('A', None)
  ```
