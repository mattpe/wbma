class: center, middle

# AJAX + state

## 1/2019

---

Study [Context](https://reactjs.org/docs/context.html), [State Hook](https://reactjs.org/docs/hooks-state.html), [Effect Hook](https://reactjs.org/docs/hooks-effect.html) and [this article](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
* We'll use the coding method in the article as an example to do the following tasks 

# Fetching data with AJAX, Task A

1. Continue last exercise. Create a new branch `http-a` with git and checkout it (`git checkout -b http-a`).
1. TODO_CONTEXT_API_HOWTO
1. [test.json](./assets/test.json) url = https://raw.githubusercontent.com/mattpe/wbma/master/docs/assets/test.json
1. In App.js, use [fetch](https://ilkkamtk.github.io/SSSF-course/Slides/JS%20recap/W1-2-JavaScript-cheat.html) or axios to load test.json
    - fetch is used in teacher's examples
    - 
    - prevent fetch from looping by using [cleanup](https://medium.com/@selvaganesh93/how-to-clean-up-subscriptions-in-react-components-using-abortcontroller-72335f19b6f7)
        - read Cleanup in hooks
1. First log the data using `console.log()`
    * [Debugging JavaScript](https://docs.expo.io/versions/v34.0.0/workflow/debugging/#debugging-javascript)
1. Save the data to state and then print the data to the list made in last exercise
1. git add, commit & push to remote repository

---

# Fetching data with AJAX, Task B

1. Continue last exercise. Create a new git branch `http-b` and use it.
1. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](http://media.mw.metropolia.fi/wbma/docs/)
    - base url: http://media.mw.metropolia.fi/wbma/
    - Media files location: http://media.mw.metropolia.fi/wbma/uploads/
1. First log the data using ```console.log()```
    - Note that '/media' endpoint doesn't give you thumbnails. You need to do a nested request to '/media/:id' to get also thumbnails.
        - Study Promise.all [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) and [here](http://promise-nuggets.github.io/articles/14-map-in-parallel.html)
        - example: 
        ```javascript
        // 2nd fetch:
        Promise.all(array.map(item => {
            return fetch(url + item.id).
                then(response => {
                  return response.json();
                });
          })).then(items => {
            console.log(items);
            // save items to state
          });
        ```
1. Save the data to state and then print the data to the table
1. git add, commit & push to remote repository
