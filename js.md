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

## Strings
### Capitalize

```
function capitalize(str){
  if (!str.length) return ""
  return str.charAt(0).toUpperCase().concat(str.slice(1).toLowerCase())
}
```

### Object to url params
```
const params = { filter: false, id: 100, cool: 'beans' }

Object.entries(params)
  .reduce((acc, [key, value]) => [...acc, `${key}=${value}`], [])
  .join('&')
```

### Boolean key:value to array of keys
```
const siqObj = {
  someKey: true,
  someFalseKey: false,
  anotherKeyForGoodMeasure: true,
}

const toKeyArray = obj => 
  Object.entries(obj)
    .map(([key, value]) => !!value ? key : null)
    .filter(i => !!i)
    
console.log(toKeyArray(siqObj))   
// outputs ['someKey', 'anotherKeyForGoodMeasure']
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

### Change position of an element (without splice)
```
const list = ['A', 'B', 'C', 'D', 'E', 'F']
const target = 4
const newPosition = 2
function moveItem(list, target, newPosition){
  const without = list.filter((_, index) => index != target)
  return [
    ...without.slice(0, newPosition),
    list[target],  
    ...without.slice(newPosition, without.length)
  ]
}

console.log(moveItem(list, target, newPosition))
// outputs: ['A', 'B', 'E', 'C', 'D', 'F'] 
```

## Math
### Round to nearest half
```
function roundToNearestHalf(value) {
  return (Math.round(value * 2) / 2).toFixed(1);
}
```

## Dates
### Generate month names (with moment)
```
[...Array(12).keys()].map(m => moment(m+1, "MM").format("MMM"))
// returns ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
```

## Async / Await / Promises / Callbacks
### Async IIFE
```
(async function(){
  await somethingCool()
})()
```
### Wait for parallel async functions
```
// executes each iteration in parallel
const arr = [ ... ]
async someFunction = () => { ... }

await Promise.all(arr.map(someFunction))
```

### Wait for sequential async functions
```
// executes each iteration in series
const arr = [ ... ]
async someFunction = () => { ... }

for (item of arr){
  await someFunction(item)
}
```
