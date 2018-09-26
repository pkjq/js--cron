[![NPM](https://nodei.co/npm/cron-pkjq.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/cron-pkjq/)

# CRON
Scheduler with cron syntax

## Installation

- `npm install cron-pkjq`

## Usage

In Node.js:

```javascript
const cron = require("cron-pkjq");

let newYearCron = cron.add('@yearly', () => { console.log('Happy new year!!!'); });


// cron may be stopped
cron.stop(newYearCron);

// and may be started again
cron.start(newYearCron);
```


## Syntax
This implementation uses [cron-parser](https://github.com/harrisiirak/cron-parser) for parse cron-expressions. Supported syntax should be looked there.
You may use [crontab.guru](https://crontab.guru) to check your cron-expression.


### Quick reference to supported cron syntax:

The format is a five(or six) time-and-date fields or a predefined macros with prefix '@'.
Commands will be executed when the 'minute', 'hour', and 'month of the year' fields match the current time, and at least one of the two 'day' fields ('day of month', or 'day of week') match the current time.
The day of a command's execution can be specified in the following two fields - 'day of month', and 'day of week'. If both fields are restricted (i.e., do not contain the "*" character), the command will be run when either field matches the current time.

#### fields format

```
  ┌─────────────── second (optional)
  │  ┌──────────── minute
  │  │ ┌────────── hour
  │  │ │ ┌──────── day of month
  │  │ │ │ ┌────── month
  │  │ │ │ │ ┌──── day of week
 [*] * * * * *
```

#### values

|     field    |         value        |
|:--------------:|:----------------------:|
|    second    |          0-59        |
|    minute    |          0-59        |
|     hour     |          0-23        |
| day of month |          1-31        |
|     month    |          1-12 or short names        |
| day of week  |         0-7          (0 and 7 are sunday)  or short names    |

A field may contain an asterisk (*), which always stands for "first-last".

#### multiples values and ranges

Ranges of numbers are allowed. Ranges are two numbers separated with a hyphen. The specified range is inclusive. For example, 8-11 for an 'hours' .

```javascript
cron.schedule('* 8-10 * * *', () => { console.log('entry specifies execution at hours 8, 9, 10, and 11'); });
```

Lists are allowed. A list is a set of numbers (or ranges) separated by commas. Examples: "1,2,5,9", "0-4,8-12".

```javascript
cron.schedule('1,2,4,5 * * * *', () => { console.log('entry specifies execution every minute 1, 2, 4, 5'); });
```

Step values can be used in conjunction with ranges. Following a range with "/<number>" specifies skips of the number's value through the range. For example, "0-23/2" can be used in the 'hours' field to specify command execution for every other hour. Step values are also permitted after an asterisk, so if specifying a job to be run every two hours, you can use "*/2".
  
```javascript
cron.schedule('*/2 * * * *', () => { console.log('every 2 minutes'); });
```

Names can also be used for the 'month' and 'day of week' fields. Use the first three letters of the particular day or month (case does not matter).
But ranges or lists of names are not allowed.

#### macros

|macros|equivalent|comment|
|:-:|:-:|:-|
|@hourly|'0 * * * *'||
|@daily|'0 0 * * *' | At 12:00am|
|@weekly|'0 0 * * 0'| At 12:00am on Sunday|
|@monthly|'0 0 1 * *'| 1st of every month at 12:00am |
|@yearly|'0 0 1 1 *'| 1st January every year at 12:00am |


#### short names of month

|№|month|
|:-:|:-:|
|1|jan|
|2|feb|
|3|mar|
|4|apr|
|5|may|
|6|jun|
|7|jul|
|8|aug|
|9|sep|
|10|oct|
|11|nov|
|12|dec|

#### short names of day of weak

|№|day of weak|
|:-:|:-:|
|0|sun|
|1|mon|
|2|tue|
|3|wed|
|4|thu|
|5|fri|
|6|sat|
|7|sun|

---
*About copyrights read legal_notice, please!*
