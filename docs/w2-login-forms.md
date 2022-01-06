# Login and Register forms

1. Study [useState with forms](https://www.youtube.com/watch?v=R7T5GQLxRD4)
2. Study [React Native Forms using React-Hook-Form](https://www.akashmittal.com/react-native-forms-using-react-hook-form/)
3. Continue last exercise. Create a new branch 'forms' with git.
### A. Fetch token from Media API

1. Recap how to make [POST request with fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Supplying_request_options)
2. [Login endpoint in the Media API](http://media.mw.metropolia.fi/wbma/docs/#api-Authentication-PostAuth)
3. Add a new hook called _useLogin_ to ApiHooks.js. Add a new function _postLogin_ to _useLogin_ hook:
  ```jsx harmony
   // ApiHooks.js
   ...
   const useLogin = () => {
  
      const postLogin = async (userCredentials) => { // user credentials format: {username: 'someUsername', password: 'somePassword'}
         const options = {
            // TODO: add method, headers and body for sending json data with POST
         };
         try {
            // TODO: use fetch to send request to login endpoint and return the result as json, handle errors with try/catch and response.ok
         } catch (error) {
            throw new Error(error.message);
         }
      };
      
      return {postLogin};
   };
   ...
  ```
5. Modify _logIn_ function in _Login.js_. The function should call postLogin in useLogin hook to get the userdata and token from the API
   ```jsx harmony
   // Login.js
   ...
   const logIn = async () => {
     // hard code your username and password:
     const data = {username: 'someUsername', password: 'somePassword'};
      // TODO: call postLogin
      // TODO: if login succesful do the following:
     await AsyncStorage.setItem('userToken', tokenFromApi);
     setIsLoggedIn(true);
     navigation.navigate('Tabs');
   };
   ...
   ```
6. Test the Login button and then reload the app. The app should login, but it does not remember the you have logged in after reloading.
7. Add new hook _useUser_ to ApiHooks.js and a new function _getUserByToken_ to _useUser_:
   ```jsx
   const useUser = () => {
   
    const getUserByToken = async (token) => {
      try {
        const options = {
          method: 'GET',
          headers: {'x-access-token': token},
        };
        const response = await fetch(baseUrl + 'users/user', options);
        const userData = response.json();
        if (response.ok) {
          return userData;
        } else {
          throw new Error(userData.message);
        }
      } catch (error) {
        throw new Error(error.message);
      }
    };
   
    return {getUserByToken};
   };
   ```
8. Modify _checkToken_ function in _Login.js_. The function should call _getUserByToken_ function with the saved _userToken_. Then allow or deny access to the app.
   ```jsx
   const checkToken = async () => {
       const userToken = await AsyncStorage.getItem('userToken');
       console.log('token', userToken);
       // TODO: call getUserByToken(userToken), if you get successful result, set isLoggedIn to true and navigate to Tabs
     };
   ```

### B. Login and Register forms  
 
1. Create LoginForm.js to components folder. Use ['React Native demo'](https://react-hook-form.com/get-started#ReactNative) as an example and create a form with two fields: 'username' and 'password'. Set both fields as required and log the contents to console when submit button is pressed.
2. Add LoginForm component to Login.js:
    ```jsx harmony
    const Login = ({navigation}) => {
    ...   
    return (
        <View style={styles.container}>
          <Text>Login</Text>
          <LoginForm navigation={navigation}/>
        </View>
      );
   ...
   ```
3. Fill the form and press submit button and check the log.
4. To use the form for the login functionality move the logic from _logIn_ function in Login.js to _onSubmit_ function in LoginForm.js. Remember to update the imports etc.
5. The login form should now work.
6. You might want to change some [props of the TextInputs](https://reactnative.dev/docs/textinput#props) to secure the password field and get rid of automatic capitalisation and maybe add placeholders.
7. Create new file 'RegisterForm.js' to components folder. Use LoginForm.js as an example and add four fields username, password, email and full_name and submit button. All fields except full_name are required.
8. Add _RegisterForm_ component to Login.js:
   ```jsx
   // Login.js
   ...
   return (
    <View style={styles.container}>
      <Text>Login</Text>
      <LoginForm navigation={navigation}></LoginForm>
      <RegisterForm></RegisterForm>
    </View>
   );
   ...
   ```
9. Add new function _postUser_ to _useUser_ hook in ApiHooks.js: 
   ```jsx
   // ApiHooks.js
   ...
   const postUser = async (data) => {
    const options = {
      // TODO: add method, headers and body for sending json data with POST
    };
    try {
      // TODO: use fetch to send request to users endpoint and return the result as json, handle errors with try/catch and response.ok
    } catch (error) {
      throw new Error(error.message);
    }
   ...
   ```
10. Test that you can create new users with _RegisterForm_
11. Add the final functionalities:
    * when logging in, save user data to [Context](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react). With Context you can create a global state which can be accessed from all components. Token is still saved to AsyncStorage.
    * Modify MainContext.js:
    ```jsx
    ...
    const MainProvider = ({children}) => {
        const [isLoggedIn, setIsLoggedIn] = useState(false);
        const [user, setUser] = useState({});
    
        return (
          <MainContext.Provider value={{isLoggedIn, setIsLoggedIn, user, setUser}}>
            {children}
          </MainContext.Provider>
        );
      };
      ...
      ```
    * <b>Note the change from [] to {} in MainContext.Provider value</b>. This means that you need to change square brackets to curly braces everywhere where you have `const [isLoggedIn, setIsLoggedIn] = useContext(MainContext);`
    * Setting user data example:
    ```javascript
    // now the vars and funcs can be in any order.
    const {setUser, isLoggedIn, user, setIsLoggedIn} = useContext(MainContext);
    setUser(userdataFromApi.user); 
    ```
12. Use the saved user data in _Profile.js_
    - log user data to console (for debugging)
    - use [_Text_ component](https://reactnative.dev/docs/text) to display the user data on the profile page
13. Try the app on a real device. You can see that it's hard/impossible to write since keyboard is covering the input fields. Use [KeyboardAvoidingView](https://reactnative.dev/docs/keyboardavoidingview) in Login.js to fix the issue. 
14. Add and commit changes to git, push to Github/GitLab.
