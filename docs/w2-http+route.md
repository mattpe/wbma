# AJAX, Routing

## 2/2019

---

# AJAX 2, Move reusable functions to a separate file

1. Continue last exercise. Create a new branch with git.
1. Create new folder 'utils' to 'src' folder
1. In the 'utils' folder create a new file 'MediaAPI.js'
1. In 'MediaAPI.js' make function getAllMedia and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) it.
    - getAllMedia should fetch all media files and their thumbnails from MediaAPI (just like last exercise)
    * example: 
    ```javascript
    ...
    const getAllMedia = () => {    
     return fetch(apiUrl).then(param => {
     ...then(someParam => {
           return Promise.all(someParam.map(item => {
             return fetch(...
             ...
       }
    }
    ...
    export {getAllMedia}
    ```
1. In App.js use getAllMedia in componentDidMount-hook to add files to state and display the data in table the same way as last exercise.
    - when using webStorm MediaAPI.js should be auto imported. If not, import it manually.

# Routing 

Study [React crash course](https://www.youtube.com/watch?v=sBws8MSXN7A) from 1:15:48  to 1:25:44

1. Install react-router-dom with npm or yarn
1. Goal is to make a navigation between three 'pages'
    * main menu has two links: 'Home' and 'Profile'
    * Each media file has 'view' link next to it. Clicking that should take to 'Single'
1. Create new component 'Nav.js' (to components folder)
    * content for Nav.js:
    ```javascript
    import React from 'react';
    
    const Nav = () => {
      return (
          <nav>
            <ul>
              <li>
                Home
              </li>
              <li>
                Profile
              </li>
            </ul>
          </nav>
      );
    };
    
    export default Nav;
    ```
1. Add Nav-component to App.js so that you can see it above Table component in browser
1. Create new folder 'views' to folder 'src'
1. Create 'Home.js', 'Single.js' and 'Profile.js' to 'views'
    * Home.js will be the component that should show first when the app starts
    * Content for Home.js
    ```jsx harmony
    import React from 'react';
    
    const Home = (props) => {
      return (
          <React.Fragment>
            <h1>Home</h1>
          </React.Fragment>
      );
    };
    
    export default Home;
    ```
    * Move the following jsx from App.js to Home.js
    ```jsx harmony
      <Table picArray={this.state.picArray}/>
    ```
    * Replace it with
    ```jsx harmony
      <Home picArray={this.state.picArray} />
    ``` 
    * In Home.js, make the moved code to use props instead of state. Also remove `this`because Home.js is funciton component not class.
    * The app should at this point work the same as before
1. Content for Profile.js (this is a [function component](https://reactjs.org/docs/components-and-props.html#function-and-class-components)):
    ```javascript
    import React from 'react';
    
    const Profile = (props) => {
      return (
          <React.Fragment>
            <h1>Profile</h1>
          </React.Fragment>
      );
    };
    
    export default Profile;
    ```
1. Content for Single.js (this is a [class component](https://reactjs.org/docs/components-and-props.html#function-and-class-components)):
   ```javascript
   import React, {Component} from 'react';
   import PropTypes from 'prop-types';
   
   class Single extends Component {
     mediaUrl = 'http://media.mw.metropolia.fi/wbma/uploads/';
     state = {
       file: {
         filename: 'b2db3cce51674aba84d9476a545c5cc4.jpg',
         title: 'Test',
       },
     };   
   
     render() {
       return (
           <React.Fragment>
             <h1>{this.state.file.title}</h1>
             <img src={this.mediaUrl + this.state.file.filename}
                  alt={this.state.file.title}/>
           </React.Fragment>
       );
     }   
   }
   
   Single.propTypes = {
     match: PropTypes.object,
   };
   
   export default Single;
   ```
1. Study the video above and create routing described in bullet 2.
    ```jsx harmony
    // sending props to route
    <Route path="/example" render={(props) => (
                    <Example {...props} file={this.state.file}/>
                )}/>
    ```
    ```javascript
1. [three dots](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
1. To make links work also in subfolders when building add basename attribute to Route:
    ```jsx harmony
    <Router basename='/~username/foldername'>
    ```
## Show single file & local state
  
1. In 'mediaAPI.js' make function getSingleMedia and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) it.
    - getSingleMedia should fetch one media file with thumbnails from MediaAPI (just like last exercise)
    * example: 
    ```javascript
    ...
    const getSingleMedia = (id) => {
      return fetch(...
    };
    ...
    ```
1. In Tr.js make the 'view' link to open 'Single' component and send file_id as a parameter.

1. Study [react-router-dom url parameters](https://tylermcginnis.com/react-router-url-parameters/) to get file_id to Single.js
1. In Single.js receive the file_id parameter and use getSingleMedia in componentDidMount-hook to add file to state and display the title in `<h1>` element and file in `<img>` element.
1. git add, commit & push to remote repository
1. Deploy project to your public_html 

---

