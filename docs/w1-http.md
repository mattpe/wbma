class: center, middle

# AJAX + state

## 1/2019

---

Study [Context](https://reactjs.org/docs/context.html), [State Hook](https://reactjs.org/docs/hooks-state.html), [Effect Hook](https://reactjs.org/docs/hooks-effect.html) and [this article](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
* We'll use the coding method in the article as an example to do the following tasks 

## Fetching data with AJAX and sharing it with Context, Task A

1. Continue last exercise. Create a new branch `http-a` with git and checkout it (`git checkout -b http-a`).
    1. Create 'contexts' folder to project root folder
    2. Add MediaContext.js file to contexts:

        ```js
        import React, {useState} from 'react';
        import PropTypes from 'prop-types';

        const MediaContext = React.createContext([{}, () => {}]);

        const mediaArray = [];

        const MediaProvider = (props) => {
          const [media, setMedia] = useState(mediaArray);
          return (
            <MediaContext.Provider value={[media, setMedia]}>
              {props.children}
            </MediaContext.Provider>
          );
        };

        MediaProvider.propTypes = {
          children: PropTypes.node,
        };

        export {MediaContext, MediaProvider};
        ```

    3. Move mediaArray from App.js to MediaContext's state
    4. Add _MediaProvider_ to App.js JSX
    5. Modify List.js to use the data from MediaContext instead of prop

        ```js
        ...
        const [media, setMedia] = useContext(MediaContext);
        ...
        ...
        <FlatList
          data={media}
        ...
        ```

    6. Test that the app still works.
1. Use [test.json](./assets/test.json) url = https://raw.githubusercontent.com/mattpe/wbma/master/docs/assets/test.json instead of the hard coded mediaArray
   * use [fetch](https://javascript.info/async-await#await) or axios to load test.json,
     * fetch is used in the course material
     * prevent fetch from looping by using effect-hook.
     * Use 'hooks.js' from [this article](https://medium.com/@cwlsn/how-to-fetch-data-with-react-hooks-in-a-minute-e0f9a15a44d6) as an example
        * create 'hooks' folder to project root and save 'hooks.js' as 'APIHooks.js' there
        * convert functions to arrow functions.
        * In _List.js_ First log the loaded data using `console.log()`
           * [Debugging JavaScript](https://docs.expo.io/versions/v34.0.0/workflow/debugging/#debugging-javascript)
           * Use _Photos.js_ in the article as example.
        * Save the data to MediaContext's state using `setMedia`. 
        * Use [keyExtractor](https://www.techiediaries.com/react-native-tutorial/flatlist-with-renderitem-and-keyextractor/) in _List.js_ to fix the warning about missing keys
1. git add, commit & push to remote repository

---

## Fetching data with AJAX, Task B

1. Continue last exercise. Create a new git branch `http-b` and use it.
1. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](http://media.mw.metropolia.fi/wbma/docs/)
    - base url: http://media.mw.metropolia.fi/wbma/
    - Media files location: http://media.mw.metropolia.fi/wbma/uploads/
1. In _APIHooks.js_ 
   * add this after imports: `const apiUrl = 'http://media.mw.metropolia.fi/wbma/';`
   * rename useFetch function to 'getAllMedia' and remove url parameter from parens.
   * change `const response = await fetch(url);` to `const response = await fetch(apiUrl + 'media/all');`
1. First log the loaded data using ```console.log()```
   * Note that '/media/all' endpoint doesn't give you thumbnails. You need to do a nested request to '/media/:id' to get also the thumbnails. To get the file_id:s you need to iterate 'files' property from the '/media/all' endpoints response.
   * To combine multiple fetch results use [Promise.all](https://www.freecodecamp.org/news/promise-all-in-javascript-with-example-6c8c5aea3e32/):
   ```javascript
   const result = await Promise.all(array.map(async (item) => {
      const response = await fetch(url);
      return await response.json();
    }));
   ```
1. In _List.js_ use _getAllMedia_ instead of useFetch
1. git add, commit & push to remote repository
