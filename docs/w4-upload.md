# WBMA, Forms + Upload

## 9/2021

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
1. add `<Image>` and input fields for 'title' and 'description' like in LoginForm.js. Also add two buttons for selecting and uploading a file.
1. Create 'hooks/UploadHooks.js' and make hooks for title and description like in LoginHooks.js
1. Study [ImagePicker](https://docs.expo.io/versions/v34.0.0/sdk/imagepicker/) and use the example to select Image from ImagePicker and display it in `<Image>` when the first button is pressed.
1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)
    - if current version of Expo or React Native seems to have an issue with fetch using FormData try [Axios](https://github.com/axios/axios) instead. Currently (9/21) fetch seems to be working.
    - in Upload.js create functon 'doUpload' which is called by onPress event of the second button (a bit like in _Login.js_).
       - you can use [this article](https://stackoverflow.com/questions/42521679/how-can-i-upload-a-photo-with-expo) as a reference (use Axios instead of fetch). See the part after this comment "// ImagePicker saves the taken photo to disk and returns a local URI to it". NOTE: the example generates an invalid [mime-type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types#JPEG) for `.jpg` files. This can be fixed e.g. ("quick'n'dirty" style) by adding a row `if (type === 'image/jpg') type = 'image/jpeg';` after the `let type = ...` statement
       - !!IMPORTANT!! In iOS type can be just 'image' or 'video' etc. Android requires full MIME type like 'image/png'. That is why there is 'Infer the type of the image' in the article above.
    - display an [`<ActivityIndicator>`](https://reactnative.dev/docs/activityindicator) when file is being uploaded
1. After the file is uploaded (promise returned by async upload function is completed) redirect to Home
    - there might be a need to wait 1-2 seconds before going to Home so that thumbnail (generated on the server) is ready
    - after [navigating](https://reactnavigation.org/docs/navigation-actions/#navigate) to Home-view the file list must be refreshed to see new files
      - add a new state to _MainContext_ to control the file list refreshing
      - modify _useEffect()_ hook inside _useLoadMedia()_ hook to react when that state changes
1. Upload button should be activated only when the form is correctly filled and media file is selected
    - Title is required and minimun length is ?
    - Description minimun length is ?
    - Hint: Button component has property 'disabled'  
1. Add reset button for clearing the whole form and image preview
    - also reset the form after file is uploaded.
    
### Task B: List files limiting to those uploaded from your own app

1. Come up with an unique identifier for your app. It can be anything. For example _LH345D_. 
1. When uploading add the identifier as a [tag](http://media.mw.metropolia.fi/wbma/docs/#api-Tag-PostTag) to the uploaded file.
1. Modify useAllMedia() in ApiHooks.js to show only the files which have the identifier tag of your app.

### Extra: Additional features

1. Show [spinners](https://docs.nativebase.io/Components.html#Spinner) when loading and uploading data
1. Could the code be cleaner? Maybe put some JSX into separate files (to components folder)
