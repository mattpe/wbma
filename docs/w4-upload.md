class: center, middle

# WBMA, Forms + Upload

## 4/2019

---

# Forms

### Task A: Create Upload Form 

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Study [Expo SDK](https://docs.expo.io/versions/v34.0.0/sdk/overview/)
1. Install required Expo SDK components:
   - `expo install expo-image-picker`
   - `expo install expo-permissions`
   - `expo install expo-constants`
1. Create a new file 'views/Upload.js' for the upload functionality
1. Add a button to bottom tabs to navigate to Upload component
1. add `<Image>` and input fields for 'title' and 'description' like in Login.js. Also add two buttons for selecting and uploading a file.
1. Create 'hooks/UploadHooks.js' and make hooks for title and description like in LoginHooks.js
1. Study [ImagePicker](https://docs.expo.io/versions/v34.0.0/sdk/imagepicker/) and use the example to select Image from ImagePicker and display it in `<Image>` when the first button is pressed.
1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects) 
    - in UploadHooks.js create functon 'handleUpload' which is called by onPress event of the second button. The function should receive the selected image as a parameter.
       - you can use [this article](https://stackoverflow.com/questions/42521679/how-can-i-upload-a-photo-with-expo) as a reference. See the part after this comment "// ImagePicker saves the taken photo to disk and returns a local URI to it" 
    - After image is uploaded redirect to Home
        - refresh image table to update the list. It might be neccessary to empty the 'media' array of the context before loading the updated content to it or the list might not render properly.
        - wait 2 seconds before going to Home so that thumbnail is ready
1. Upload button should be activated only when the form is correctly filled and media file is selected
    - Title is required and minimun length is ?
    - Description is optional but minimun length is ?
1. Add reset button for clearing the whole form and image preview    
        
### Extra: Use OpenGL to add filters to image
1. Study [gl-react-expo](https://www.npmjs.com/package/gl-react-expo)
1. Do a new app where user can select existing picture or take a new picture with phone's camera and then edit brightness, contrast and saturation (of course tou can add the functionalities to the existing app instead)
   - [Example](https://github.com/gre/gl-react/tree/master/examples/expo-gl-react-camera-effects)
1.[More examples](https://gl-react-cookbook.surge.sh/)