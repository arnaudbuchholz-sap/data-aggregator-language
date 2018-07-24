# Data Aggregator

Execute aggregation expressions on a given data set.

# What it Does
Given the following input data structure,
```js
const input = [{ 
  date: '2017-09-16',
  reservations: {
    silver: 12,
    gold: 5
  }  
}, {
  date: '2017-09-17',
  reservations: {
    silver: 3,
    gold: 2
  }  
}]
```
the parser allows mixing aggregation expressions over the input with common arithmetic operators.

For example,
* an aggregation expression: `SUM reservations.silver` would yield `12 + 3 = 15`.
* an aggregation expression mixed with arithmetic: `SUM reservations.silver + 3` would yield `(12 + 3) + 3 = 18`
# Usage
```js
const aggregator = require('@emartech/data-aggregator-language')(input);
const result = aggregator('SUM reservations.silver').value
```

# Supported Syntax In Aggregation Expressions

Examples below are for the `input` defined above.
## Constants
* LENGTH 
  * `LENGTH` (yields 2)
  * `LENGTH + 3` (yields 5)
* Any number literal
  * `5` (yields 5)

## Unary Operators
* SUM
  * `SUM reservations.silver` (yields 15)
* LAST
  * `LAST reservations.silver` (yields 3)
* AVERAGE
  * `AVERAGE reservations.silver` (yields 7.5)

## Binary Operators
+, -, *, /

For example, `(LAST reservations.silver + 3) * 2 / 2` (yields 6)

# Commit Convention
Semantic release depends on the [Angular commit message conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153). Please follow these.

# Credit
Uses [SAP/chevrotain](https://github.com/SAP/chevrotain) for parsing.
