class: center, middle

# WBMA, Forms + Upload

## 4/2019

---

## Forms

### Task A: Create Upload Form

1. Continue the previous exercise. Create a new git branch 'upload' for these tasks.
1. Study [Expo SDK](https://docs.expo.io/versions/latest/)
1. Install required Expo SDK components:
   - `expo install expo-image-picker`
   - `expo install expo-permissions`
   - `expo install expo-constants`
1. Create a new file 'views/Upload.js' for the upload functionality. Add function component and the usual imports and exports.
1. Add a button to bottom tabs to navigate to Upload component
1. add `<Image>` and input fields for 'title' and 'description' like in Login.js. Also add two buttons for selecting and uploading a file.
1. Create 'hooks/UploadHooks.js' and make hooks for title and description like in LoginHooks.js
1. Study [ImagePicker](https://docs.expo.io/versions/v34.0.0/sdk/imagepicker/) and use the example to select Image from ImagePicker and display it in `<Image>` when the first button is pressed.
1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)
    - current version of Expo or React Native seems to have an issue with fetch using FormData so lets try [Axios](https://github.com/axios/axios) instead 
    - in Upload.js create functon 'doUpload' which is called by onPress event of the second button (a bit like LoginForm.js).
       - you can use [this article](https://stackoverflow.com/questions/42521679/how-can-i-upload-a-photo-with-expo) as a reference (use Axios instead of fetch). See the part after this comment "// ImagePicker saves the taken photo to disk and returns a local URI to it". NOTE: the example generates an invalid mime-type for `.jpg` files. This can be fixed e.g. ("quick'n'dirty" style) by adding a row `if (type === 'image/jpg') type = 'image/jpeg';` after the `let type = ...` statement
    - After image is uploaded (promise returned by async upload function is completed) redirect to Home
        - wait 1-2 seconds before going to Home so that thumbnail (generated on the server) is ready
        - when going to Home-view use [push](https://reactnavigation.org/docs/stack-actions/#push) instead of [navigate](https://reactnavigation.org/docs/navigation-actions/#navigate). Why? 
  
1. Upload button should be activated only when the form is correctly filled and media file is selected
    - Title is required and minimun length is ?
    - Description is optional but minimun length is ?
    - Hint: Button component has property 'disabled'  
1. Add reset button for clearing the whole form and image preview
    - also reset the form after file is uploaded.
    
### Task B: List files limiting to those uploaded from own app
1. Come up with an identifier for your app. It can be anything. For example LH345D
1. When uploading add the identifier as a tag to the uploaded file.
1. Modify useAllMedia() in ApiHooks.js to show only the files which have the identifier tag of your app.

### Extra: Additional features

1. Show spinners when loading and uploading data
1. Could the code be cleaner? Maybe put some JSX into separate files (to components folder)
