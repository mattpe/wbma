# JavaScript Promise

---

## Asynchronous JavaScript
* JavaScript is single threaded
   * Synchronous function puts the whole process on wait until it's completed
   * This is why AJAX-calls, database queries, file handling etc. are done asynchronously
     * Instead returning a something from a function we get the response as a parameter of a callback function

---

### Synchronous function ([source](https://www.promisejs.org))
```
function readJSONSync(filename) {
  return JSON.parse(fs.readFileSync(filename, 'utf8'));
}
```

### Asynchronous function ([source](https://www.promisejs.org))
```
function readJSON(filename, callback){
  fs.readFile(filename, 'utf8', function (err, res){
    if (err) return callback(err);
    callback(null, JSON.parse(res));
  });
}
```

---

### Getting error messages gets a bit complicated
```
function readJSON(filename, callback){
  fs.readFile(filename, 'utf8', function (err, res){
    if (err) return callback(err);
    try {
      res = JSON.parse(res);
    } catch (ex) {
      return callback(ex);
    }
    callback(null, res);
  });
}
```

---

##Promise
* Promise is an object that promises to return a value
* Promise has three states
 1. Pending: initial state
 2. Resolved: promise fulfilled
   * Promise has a value
 3. Rejected: promise unfulfilled
   * Promise has a reason (why it failed)

![alt text](http://i.stack.imgur.com/JzrAY.png "Promise")

### Creating a promise:
```
function readFile(filename, enc){
  return new Promise(function (fulfill, reject){
    fs.readFile(filename, enc, function (err, res){
      if (err) reject(err);
      else fulfill(res);
    });
  });
}
```

---

## Promise.then
* Promise object has a method 'then' which can be used to chain promises
* then gets two parameters as functions
  *  onFulfilled
    * when the promise has been fulfilled
  * onRejected
    * when the promise has not been fulfilled
* then returns a new promise
  * return value depends on the original promise object and onFulfilled or onRejected functions
  
---
### Examples
## readJson using promise
```
function readJSON(filename){
  return readFile(filename, 'utf8').then(function (res){
    return JSON.parse(res)
  })
}
```
## Same function, shorter version
```
function readJSON(filename){
  return readFile(filename, 'utf8').then(JSON.parse);
}
```
