# JS
## Concepts
### Call / Apply / Bind
```
const param = { whoIsAwesome: 'YOU!' }

function awesome(howAwesome){
  console.log(`${this.whoIsAwesome} are ${howAwesome} awesome!`)
}

function maxAwesome(){
  console.log(`${this.whoIsAwesome} are ultra awesome!`)  
}
```
* `.call()` invokes the function and allows you to pass in arguments one by one.
```
awesome.call(param, 'pretty')
```
* `.apply()` invokes the function and allows you to pass in arguments as an array.
```
awesome.apply(param, ['super'])
```
* `.bind()` returns a new function, allowing you to pass in a this array and any number of arguments.
  - Bind returns a new function. call and apply execute the current function immediately.
```
const ultraAwesome = maxAwesome.bind(param)
ultraAwesome()
```

## Environments
### Environment checks
```
function isBrowser(){
  // TODO: what is the proper way to check this?
  return typeof window !== 'undefined';
}

function isNode(){
  return typeof window === 'undefined' && typeof process !== 'undefined';
}

function isCli(){
  return require.main === module;
}
```

## Padding

So it turns out filling an array with the character you would like to use for padding, [is fast](https://jsperf.com/string-padding-performance)
```
function padder(str, minlength = 3, pad = "0"){
  // naive implementation for leftpad
  if (String(str).length >= minlength) return String(str);
  const padder = Array(minlength + 1).join(pad); // make an empty array of arbitrary length, filled with zeros
  // extract the number of padded characters we want, then add them infront of the string
  return padder.substring(0, padder.length - String(str).length) + str;
}

function zeropad(str, minlength){
  return padder(str, minlength);
}

zeropad("10", 10);
```

## Arrays
### Fill an n-sized array with a particular value
```
const n = 5
const value = 10
console.log(Array(n).fill(value))
// prints [10,10,10,10,10]
```

### Array of n items with values 0...n-1
Use the spread array operator
```
[...Array(n).keys()]
```

## Math
### Round to nearest half
```
function roundToNearestHalf(value) {
  return (Math.round(value * 2) / 2).toFixed(1);
}
```
