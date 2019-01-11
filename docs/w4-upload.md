class: center, middle

# WBMA, Angular Forms + Upload

## 3/2018

---

# Forms

### Task: Create Upload Form 

1. Use your own version of the previous [exercise](w3-login.md) as a starting point and develop it further
    - or load teachers example from Oma (w3t1.zip)
1. Create a new component for the upload functionality
    - add `<input type=file>` and `<button>Upload</button>` to the template
1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects) 
    - in previous exercise you got field values with ngModel. When sending a file, you need to use $event (event object)
    - in *.component.ts create a method which is called by (change) event of the input element. In the function log event to console to find out how to get the property that has the file. Save the value of that property to a variable of type File. 
    - create another method to upload the file. create new FormData object, add the file, title and description to the object and send it to the API using MediaService. Of course you need to create a new method to MediaService.
    
