# JavaScript Promise
## Asynchronous JavaScript
  * JavaScript is single threaded
    * Synchronous function puts the whole process on wait until it's completed
    * This is why AJAX-calls, database queries, file handling etc. are done asynchronously
      * Instead returning a something from a function we get the response as a parameter of a callback function
      
### Asynchronous function
```
Something.save(function(err) {  
  if (err)  {
    //error handling
    return;
  }
  console.log('success');
});
```
