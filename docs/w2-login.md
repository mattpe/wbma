# Login, Register

## 2/2019

# Login

1. Install [React Develper Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) to Chrome
1. Continue last exercise. Create a new branch with git.
1. Create 'Login.js' and 'Logout.js' to 'views'
    * This will be the login and register page
    * Make it to be a class component
    * Add two forms:
        * Login form with username and password fields and submit button
        * Register form with username, password, email and full name fields and submit button
        * Add local state to Login.js
        ```javascript
        state = {
            username: '',
            password: '',
            email: '',
            full_name: '',
          };
        ````
    * When login or register form is submitted, add values from corresponding form fields to local state. This way you can use them to login or register functionalities. Example:
    ```jsx harmony
    <input type="text" name="username" placeholder="username"
                     value={this.state.username}
                     onChange={this.handleInputChange}/>
    ```
    ```javascript
    handleInputChange = (evt) => {
       const target = evt.target;
       const value = target.value;
       const name = target.name;
    
       console.log(value, name);
    
       this.setState({
         [name]: value,
       });
     };
    ```
    * Change routing so that Login is shown first instead of Home
    

1. In MediaApi.js create methods 'register', 'login' and 'checkIfUserNameExists' with corresponding functionalities
    * Login.js: call MediaApi.js's functions to login user and save userdata from the API to App.js's state
        * when logged in, user is redirected to 'Home'
        * display user's info (username, fullname and email) in Profile.js
        * if user has already logged in, redirect to 'Home' (autoredirect)
            * for this, save token to [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) when logging in. Then when the app starts, use [/users/user](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetCurrentUser) endpoint to check if the token is valid
    * Register.js: call media API to create new user 
        * login automatically after registering
        * check if username already exists before trying to register
    * Logout.js: logout (clear localstorage, clear user in App.js's state, redirect to Home)
        * study [conditional rendering](https://reactjs.org/docs/conditional-rendering.html)
        * when user is logged in show Profile and Logout links in Nav. When user is logged out, hide Profile and Logout and show Login.


---

