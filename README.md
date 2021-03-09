# seq.mjs

A JavaScript module that allows iterators to use array-like methods.

There is also an asynchronous version: https://github.com/haiix/aseq

## Installation

```
npm install @haiix/seq
```

## Usage

```javascript
import seq from '@haiix/seq'
```

## Examples

1.  By passing the natural number N to the seq function, an iterator is created that increments between 0 and N.
    You can use array-like methods (map, join, etc.) on the created iterator.

    ```javascript
    seq(3).join() // "0,1,2"
    ```

    ```javascript
    seq(4).map(x => x + 1).join() // "1,2,3,4"
    ```

2.  You can pass an iterable object (with the [Symbol.iterator] method) to the seq function.

    ```javascript
    seq([10, 20, 30]).map(x => x + 1).join() // "11,21,31"
    ```

3.  There are no methods implemented that rewrite themselves.
    If you want to use those methods, convert them to arrays once.

    ```javascript
    //seq(5).reverse() // Error
    Array.from(seq(5)).reverse() // [4, 3, 2, 1, 0]
    ```

4.  In this example, the array is not created internally, and the map and filter operations for terms after 5 found in indexOf are not performed.

    ```javascript
    seq(100).map(x => x * 2).filter(x => x % 3 > 0).indexOf(16) // 5
    ```

5.  The iterator created by the seq function can be used in a for-of statement.
    Use in processing with side effects.

    ```javascript
    for (const n of seq(3)) {
      console.log(n) // 0, 1, 2
    }
    ```

    ```javascript
    for (const elem of seq(3).map(n => document.createElement('input'))) {
      document.body.appendChild(elem)
    }
    ```
