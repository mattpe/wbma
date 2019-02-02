class: center, middle

# WBMA, Forms + Upload

## 4/2019

---

# Forms

### Task: Create Upload Form 

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Add a button to HomePage to navigate to UploadPage ([navCtrl.push](https://ionicframework.com/docs/v3/api/navigation/NavController/))
1. Create a new page for the upload functionality
    - add input fields for 'title' (type=text), 'description' (textarea) and 'file' (type=file) to the template
1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects) 
    - in previous exercise you got field values with ngModel. When sending a file, you need to use $event (event object)
    - in upload.ts create a method which is called by (change) event of the input element. In the function log event to console to find out how to get the property that has the file. Save the value of that property to a variable of type File. 
    - create another method to upload the file. create new FormData object, add the file, title and description to the object and send it to the API using MediaProvider. Of course you need to create a new method to MediaProvider.
    - Add [LoadingController](https://ionicframework.com/docs/v3/api/components/loading/LoadingController/) to show a spinner
    - After image is uploaded go back to HomePage ([navCtrl.pop](https://ionicframework.com/docs/v3/api/navigation/NavController/))
        - wait 2 seconds before going back so that thumbnail is ready
        - hide spinner
        - when back in HomePage, refresh images (use ionViewDidEnter instead of ionViewDidLoad)
    
