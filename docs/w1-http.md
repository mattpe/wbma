# AJAX + state

W1/2020

---

Study following videos: [Understanding and handling API requests](https://www.youtube.com/watch?v=2N9iqkWfjC8&list=PLDIXF8nb0VG1v4S-smVy7GV0MHsJ3PJiL&index=7) (~24 min) and [Using Hooks](https://www.youtube.com/watch?v=rEFYriigJ5A&list=PLDIXF8nb0VG1v4S-smVy7GV0MHsJ3PJiL&index=9) (~40 min)

Study [State Hook](https://reactjs.org/docs/hooks-state.html), [Effect Hook](https://reactjs.org/docs/hooks-effect.html) 

## Fetching data with AJAX, Task A

1. Continue last exercise. Create a new branch `http-a` with git and checkout it (`git checkout -b http-a`).
1. Remove mediaArray from List.js. We will load the data from a static json file instead.
1. In List.js, use [fetch](https://ilkkamtk.github.io/SSSF-course/Slides/JS%20recap/W1-2-JavaScript-cheat.html) to load [test.json](./assets/test.json)
    - Add the new code to `List` component:
    ```javascript
      const url = 'https://raw.githubusercontent.com/mattpe/wbma/master/docs/assets/test.json';
      let mediaArray = [];
       const loadMedia = async () => {
         const response = await fetch(url);
         const json = await response.json();
         console.log(json);
       };

       loadMedia();
    ```
1. Open the [developer menu](https://docs.expo.io/workflow/debugging/#developer-menu) in your device.
    - Enable Remote Debugging, open console in the browser window that opens and then reload app.
    - Why aren't the images etc. not showing anymore? Where does React get its name from? What is state?
1. Save the loaded data to state and try to get the image list back.
    - convert `let mediaArray...` to state with `useState` -hook
    - set the value of `mediaArray` state to `json` 
    - what do you see in the console?
1. Prevent infinite loop with [useEffect](https://www.robinwieruch.de/react-hooks-fetch-data).
1. Use [try/catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch) to catch possible errors from promises.
1. Use [keyExtractor](https://www.techiediaries.com/react-native-tutorial/flatlist-with-renderitem-and-keyextractor/) in _List.js_ to fix the warning about missing keys
1. git add, commit & push to remote repository

---

## Fetching data with AJAX, Task B

1. Continue last exercise. Create a new git branch `http-b` and use it.
1. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](https://media.mw.metropolia.fi/wbma/docs/)
    - base url: https://media.mw.metropolia.fi/wbma/
    - Media files location: https://media.mw.metropolia.fi/wbma/uploads/
1. Modify `loadMedia` function to load the data from the '/media' endpoint of the API.
1. First log the loaded data using ```console.log()```
   * Note that '/media' endpoint doesn't give you thumbnails. You need to do a nested request to '/media/:id' to get also the thumbnails. To get the file_id:s you need to iterate the '/media' endpoints response.
      * Study Promise.all [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) and [here](http://promise-nuggets.github.io/articles/14-map-in-parallel.html)
      * example: 
      ```javascript
      // 2nd fetch:
      Promise.all(array.map(async (item) => {
          const response =  await fetch(url + item.id);
          const json = await response.json();
          return json;
        }));
      ```
1. Save the data to state and then print the data to the table
1. git add, commit & push to remote repository

## Custom hooks, Task C

1. Create `hooks` folder and add there a new file `ApiHooks.js`.
1. Create a custom hook `useLoadMedia` to ApiHooks.js and move fetch related functionalities from List.js:
   ```javascript
   // TODO: add necessary imports
   const apiUrl = 'http://media.mw.metropolia.fi/wbma/';
   const useLoadMedia = () => {
     // TODO: move mediaArray state here
     // TODO: move loadMedia function here
     // TODO: move useEffect here
     return {mediaArray};
   };

   export {useLoadMedia};
   ```
1. Modify List.js:
   ```javascript
   ...
   const List = () => {
     const {mediaArray} = useMedia();
     return (
     <FlatList 
   ...
   ```
1. The app should work the same as before
1. git add, commit & push to remote repository
