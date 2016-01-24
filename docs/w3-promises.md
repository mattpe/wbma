# JavaScript Promise
## Asynchronous JavaScript
  * JavaScript is single threaded
    * Synchronous function puts the whole process on wait until it's completed
    * This is why AJAX-calls, database queries, file handling etc. are done asynchronously
      * Instead returning a something from a function we get the response as a parameter of a callback function
      
### Synchronous function ([source](https://www.promisejs.org))
```
function readJSONSync(filename) {
  return JSON.parse(fs.readFileSync(filename, 'utf8'));
}
```

### Synchronous function
```
function readJSON(filename, callback){
  fs.readFile(filename, 'utf8', function (err, res){
    if (err) return callback(err);
    callback(null, JSON.parse(res));
  });
}
```
