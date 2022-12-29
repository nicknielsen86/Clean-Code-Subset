# "Big-O" complexity

## Bubble sort
``` javascript
function bubbleSort(array) {
  let isSorted = false
  while(!isSorted) {
    isSorted = true
    for(let i = 0; i < array.length - 1; i++) {
      if(array[i] > array[i + 1]) {
        let value = array[i]
        array[i] = array[i + 1]
        array[i + 1] = value
        isSorted = false
      }
    }
  }
  return array
}
```

For worst case analysis of this algorithm  
we have 14n^2 + 3n + 1
For Big-O notation the final result is O(n^2)

## Euclid's algorithm to find The greatest common denominator

``` javascript
// both numbers must be greater than 0.
function euclidGCD(number1, number2) {
  if(number1 === number2) return number1
  return number1 < number2 ? euclidGCD(number1, number2 - number1) : euclidGCD(number1 - number2, number2)
}
```

For worst case analysis of this algorithm (case like euclidGCD(1, n))
we have 4n.
For Big-O notation the final result is O(n)

Here's an optimized version.
``` javascript
function euclidGCD(number1, number2) {
  if(number1 === number2) return number1
  return number1 < number2 ? euclidGCD(number1, (number2 % number1) || number1) : euclidGCD((number1 % number2) || number2, number2)
}
```
