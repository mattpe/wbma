class: center, middle

# AJAX + state

## 1/2019

---

Study [Context](https://reactjs.org/docs/context.html), [State Hook](https://reactjs.org/docs/hooks-state.html), [Effect Hook](https://reactjs.org/docs/hooks-effect.html) and [this article](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
* We'll use the coding method in the article as an example to do the following tasks 

## Fetching data with AJAX and sharing it with Context, Task A

1. Continue last exercise. Create a new branch `http-a` with git and checkout it (`git checkout -b http-a`).
    1. Create contexts folder next to components folder
    2. Add MediaContext.js file:

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
   * In _List.js_, use [fetch](https://ilkkamtk.github.io/SSSF-course/Slides/JS%20recap/W1-2-JavaScript-cheat.html) or axios to load test.json,
     * fetch is used in teacher's examples
     * prevent fetch from looping by using effect-hook. [Example](https://medium.com/@cwlsn/how-to-fetch-data-with-react-hooks-in-a-minute-e0f9a15a44d6)
   * First log the data using `console.log()`
     * [Debugging JavaScript](https://docs.expo.io/versions/v34.0.0/workflow/debugging/#debugging-javascript)
   * Save the data to MediaContext's state using `setMedia` and then print the data to the list made in last exercise
1. git add, commit & push to remote repository

---

## Fetching data with AJAX, Task B

1. Continue last exercise. Create a new git branch `http-b` and use it.
1. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](http://media.mw.metropolia.fi/wbma/docs/)
    - base url: http://media.mw.metropolia.fi/wbma/
    - Media files location: http://media.mw.metropolia.fi/wbma/uploads/
1. First log the data using ```console.log()```
    - Note that '/media' endpoint doesn't give you thumbnails. You need to do a nested request to '/media/:id' to get also the thumbnails.
1. Save the data to MediaContext's state and then print the data to the table
1. git add, commit & push to remote repository
