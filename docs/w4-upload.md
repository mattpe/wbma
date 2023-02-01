# Forms & File Upload

## Task A: Create Upload Form

1. Continue the previous exercise. Merge it to _main_ branch and create a new development branch _upload_ with git for these tasks.
2. Study [Expo SDK](https://docs.expo.io/versions/latest/)
3. Create a new file _views/Upload.js_ for the upload functionality. Add function component and the usual imports and exports.
4. Add a new tab to bottom tab navigator for navigating to `Upload` component
5. Add input fields for `title` and `description` like in the _LoginForm.js_. Add two buttons for selecting and uploading a file. Add an `<Image>` component to show a preview of the selected image.
6. Add new function `postMedia()` to `useMedia` hook in _ApiHooks.js_. The new function should send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#uploading_a_file) to the [media endpoint of the API](https://media.mw.metropolia.fi/wbma/docs/#api-Media-PostMediaFile) 
7. Study [ImagePicker](https://docs.expo.dev/versions/latest/sdk/imagepicker/) and use the example to select an image from `ImagePicker` and display it in `<Image>` when the first button is pressed.
   1. When uploading a file to the API, you need to send [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)
      - When appending file to FormData the object format is like this:
      ```jsx
      formData.append('file', {
        uri: uri, 
        name: originalFileName,
        type: mimeTypeOfFile,
      });
      ```
      - `uri:` get this from `ImagePicker` object that is stored in state
      - `originalFileName:` get this from `ImagePicker` object that is stored in state
      - `mimeTypeOfFile:` [MIME type/Media Type](https://en.wikipedia.org/wiki/Media_type) e.g. _image/jpeg_ or _video/mov_. You can get the first part from `type` of the `ImagePicker` object, the second part from `filename`

8. Send data with `onSubmit` function
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
9. Display an [`<ActivityIndicator>`](https://reactnative.dev/docs/activityindicator) when file is being uploaded or if you are using `<Button>` from React Native Elements, you can use [loading](https://reactnativeelements.com/docs/components/button#button-with-loading-spinner) prop. You'll need to add a new state (e.g. _loading_) to achieve this.
10. After the file is uploaded (promise state returned by the async upload function is _fulfilled_) redirect to _Home_ tab
    - there might be a need to wait 1-2 seconds before going to Home so that thumbnail (generated on the server) is ready. So use [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout) or [Alert with confirmation](https://reactnative.dev/docs/alert)
11. After [navigating](https://reactnavigation.org/docs/navigation-actions/#navigate) to _Home_ tab the file list must be refreshed to see new files
    - add a new state _update_ to _MainContext_ to control the file list refreshing. Set default value to `false`.
    - send the `update` state as a parameter of `useMedia` in _List.js_: `const {mediaArray} = useMedia(update);`
    - receive the parameter in `useMedia`: `const useMedia = (update) => {...`
    - modify `useEffect()` hook inside `useMedia()` hook to react when that state changes (hint: square brackets)
    - Now `loadMedia` is called every time the `update` state changes. Import and use `update` and `setUpdate` context states in _Upload.js_. When you have a successful upload, change the value of `update` to opposite (true/false) to trigger the update of `mediaArray`: `setUpdate(!update)`
12. Upload button should be activated only when the form is correctly filled and media file is selected
    - _Title_ is required and minimun length is ?
    - _Description_ minimun length is ?
    - Hint: Button component has a property `disabled`  
13. Add reset button for clearing the whole form and image preview
    - add a new function `resetForm()` which resets all the things you want to reset
    - call `resetForm()` when reset button is pressed
    - also call `resetForm()` after file is uploaded or user navigates away from this screen with [useFocusEffect](https://reactnavigation.org/docs/use-focus-effect/)
    
## Task B: List files limiting to those uploaded from your own app

1. Come up with an unique identifier for your app. It can be any string. For example _LH345D_. 
1. When uploading add the identifier as a [tag](http://media.mw.metropolia.fi/wbma/docs/#api-Tag-PostTag) to the uploaded file.
1. Modify `loadMedia()` in _ApiHooks.js_ to show only the files which have the identifier tag of your app.

## Extra: Additional features

1. Show [spinners](https://docs.nativebase.io/Components.html#Spinner) when loading and uploading data
1. Could the code be cleaner? Maybe put some JSX into separate files (to components folder)
