# JS

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
