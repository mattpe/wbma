# WBMA Week 4 

## Forms & File Upload

### Task A: Create Upload Form

1. Continue the previous exercise. Create a new git branch 'upload' for these tasks.
2. Study [Expo SDK](https://docs.expo.io/versions/latest/)
3. Create a new file 'views/Upload.js' for the upload functionality. Add function component and the usual imports and exports.
4. Add a button to bottom tabs to navigate to Upload component
5. Add input fields for 'title' and 'description' like in LoginForm.js. Also add two buttons for selecting and uploading a file. Also add `<Image>` to show a preview of the selected image.
6. Add new function _postMedia_ to _useMedia_ hook in ApiHooks.js. The new function should send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#uploading_a_file) to the [media endpoint of the API](https://media.mw.metropolia.fi/wbma/docs/#api-Media-PostMediaFile) 
7. Study [ImagePicker](https://docs.expo.dev/versions/latest/sdk/imagepicker/) and use the example to select image from ImagePicker and display it in `<Image>` when the first button is pressed.
   1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)
      * When appending file to FormData the object format is like this:
      ```jsx
      formData.append('file', {
        uri: uri, 
        name: originalFileName,
        type: mimeTypeOfFile,
      });
      ```
      * uri: get this from ImagePicker object that is stored in state
      * originalFileName: get this from ImagePicker object that is stored in state
        * mimeTypeOfFile: [MIME type/Media Type](https://en.wikipedia.org/wiki/Media_type) e.g. image/jpeg or video/mov. You can get first part from type of ImagePicker object, the second part from filename
      * _NOTE!_ If current version of Expo or React Native seems to have an issue with fetch using FormData try [Axios](https://github.com/axios/axios) instead. Currently (1/22) fetch seems to be working.
8. Send data with _onSubmit_ function
   ```jsx
      // Upload.js
      ...
      const onSubmit = async (data) => {
         // TODO: if image is not selected, Alert error message and stop running this function
         // TODO: create new FormData object and append title and description
         // TODO: get filename
         // TODO: get extension
         // TODO: if extension is jpg change to jpeg because in MIME type it has to be jpeg. Hint: ternary operator
         // TODO: append image to FormData object
         // TODO: send FormData to API with postMedia() you made earlier
      }
      ...
   ```
9. Display an [`<ActivityIndicator>`](https://reactnative.dev/docs/activityindicator) when file is being uploaded or if you are using `<Button>` from React Native Elements, you can use [loading](https://reactnativeelements.com/docs/components/button#button-with-loading-spinner) prop. You'll need to add a new state (e.g. loading) to achieve this.
10. After the file is uploaded (promise returned by async upload function is completed) redirect to Home tab
    * there might be a need to wait 1-2 seconds before going to Home so that thumbnail (generated on the server) is ready. So use [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout) or [Alert with confirmation](https://reactnative.dev/docs/alert)
11. After [navigating](https://reactnavigation.org/docs/navigation-actions/#navigate) to Home-tab the file list must be refreshed to see new files
    - add a new state _update_ to _MainContext_ to control the file list refreshing. Set default value to false.
    - send the _update_ state as a parameter of _useMedia_ in List.js: `const {mediaArray} = useMedia(update);`
    - receive the parameter in _useMedia_: `const useMedia = (update) => {...`
    - modify _useEffect()_ hook inside _useMedia()_ hook to react when that state changes (hint: square brackets)
    - Now _loadMedia_ is called every time _update_ state changes. Import and use _update_ and _setUpdate_ context states in Upload.js. When you have a successful upload, change the value of _update_ to opposite (true/false) to trigger the update of mediaArray: `setUpdate(!update)`
12. Upload button should be activated only when the form is correctly filled and media file is selected
    - Title is required and minimun length is ?
    - Description minimun length is ?
    - Hint: Button component has property 'disabled'  
13. Add reset button for clearing the whole form and image preview
    - add new function _reset_ which resets all the things you want to reset
    - call _reset_ when reset button is pressed
    - also call _reset_ after file is uploaded or user navigates away from this screen with [useFocusEffect](https://reactnavigation.org/docs/use-focus-effect/)
    
### Task B: List files limiting to those uploaded from your own app

1. Come up with an unique identifier for your app. It can be anything. For example _LH345D_. 
1. When uploading add the identifier as a [tag](http://media.mw.metropolia.fi/wbma/docs/#api-Tag-PostTag) to the uploaded file.
1. Modify loadMedia() in ApiHooks.js to show only the files which have the identifier tag of your app.

### Extra: Additional features

1. Show [spinners](https://docs.nativebase.io/Components.html#Spinner) when loading and uploading data
1. Could the code be cleaner? Maybe put some JSX into separate files (to components folder)
