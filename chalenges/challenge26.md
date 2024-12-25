# Challenge #26: 🎯 Calculate the completed percentage

#### Level: `🟢 EASY`

## Instructions

Santa Claus has already delivered all the presents! Now he's reviewing the productivity reports of the elves. But there's a problem: `the Product Owner, Mrs. Claus` 🧑‍🎄✨, needs to quickly understand if the elves met the estimated times. They are doing `Agile Scream.`

To help `Mrs. Claus`, your task is to calculate the completed percentage of each task and return it rounded to the nearest whole number. This will allow her to better plan for the next Christmas and keep everyone happy.

This is the function she's expecting:

**Examples:**

```js
getCompleted('01:00:00', '03:00:00') // 33%
getCompleted('02:00:00', '04:00:00') // 50%
getCompleted('01:00:00', '01:00:00') // 100%
getCompleted('00:10:00', '01:00:00') // 17%
getCompleted('01:10:10', '03:30:30') // 33%
getCompleted('03:30:30', '05:50:50') // 60%
```

🎁 `Now Santa Claus and the elves deserve a break. We hope they enjoyed AdventJS and will recommend it to their friends!`

## Solutions

- **JavaScript**

  ```js
  function getCompleted(timeWorked, totalTime) {
    const [time1, time2] = [timeWorked, totalTime].map(timeStr => {
      const [hh, mm, ss] = timeStr.split(':')
      return +ss + +mm * 60 + +hh * 3600
    })

    return Math.round((time1 / time2) * 100) + '%';
  }
  ```

- **TypeScript**

  ```ts
  /**
  * @param {string} timeWorked - Time worked in hh:mm:ss format.
  * @param {string} totalTime - Total estimated time in hh:mm:ss format.
  * @returns {string} - The completed percentage rounded to the nearest integer with a % sign.
  */
  function getCompleted(timeWorked: string, totalTime: string): string {
    const [time1, time2] = [timeWorked, totalTime].map(timeStr => {
      const [hh, mm, ss] = timeStr.split(':')
      return +ss + +mm * 60 + +hh * 3600
    })

    return Math.round((time1 / time2) * 100) + '%';
  }
  ```

- **Python**

  ```py
  ```
