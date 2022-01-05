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
            // TODO: use fetch to send request to login endpoint return the result as json, handle errors with try/catch and response.ok
         } catch (error) {
            throw new Error(error.message);
         }
      };
      
      return {postLogin};
   };
   ...
  ```
5. Modify _logIn()_ function in _Login.js_. The function should call postLogin in useLogin hook to get the userdata and token from the API
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
     navigation.navigate('Home');
   };
   ...
   ```
6. Test the Login button and then reload the app.
7. Add new function _checkToken_ to _useLogin_
8. Modify _getToken()_ function in _Login.js_. The function should check with the API if the saved _userToken_ is valid and then allow or deny access to the app.
   ```jsx
   const getToken = async () => {
       const userToken = await AsyncStorage.getItem('userToken');
       console.log('token', userToken);
       // do async fetch to /users/user
       // you need to send userToken
       // if you get successful result 
       // set isLoggedIn to true
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
3. Add form to RegisterForm.js with username, password, email and full_name fields and submit button:
   ```jsx
   ...
   <View>
         <FormTextInput
           autoCapitalize="none"
           placeholder="username"
           onChangeText={(txt) => handleInputChange('username', txt)}
         />
         <FormTextInput
           autoCapitalize="none"
           placeholder="password"
           onChangeText={(txt) => handleInputChange('password', txt)}
           secureTextEntry={true}
         />
         <FormTextInput
           autoCapitalize="none"
           placeholder="email"
           onChangeText={(txt) => handleInputChange('email', txt)}
         />
         <FormTextInput
           autoCapitalize="none"
           placeholder="full name"
           onChangeText={(txt) => handleInputChange('full_name', txt)}
         />
         <Button title="Register!" onPress={doRegister}/>
       </View>
   ...
   ```
    
    - Create a new re-usable componet called `FormTextInput` into 'components' folder to use the same styling for all text input fields
    ```jsx
    ...
    const FormTextInput = ({style, ...otherProps}) => {
        return (
          <TextInput
            style={[styles.textInput, style]}
            {...otherProps}
          />
        );
      };

      const styles = StyleSheet.create({
        textInput: {
          height: 40,
          borderColor: '#ccc',
          borderWidth: 1,
        },
      });
    ...
    ```
   
    - Use 'CustomHooks.js' in 'Using React Hooks...' article as an example to handle form events. Instead of using 'CustomHooks.js' as filename, use 'RegisterHooks.js'
    ```javascript
    // RegisterHooks.js:
    import {useState} from 'react';
    
    const useSignUpForm = (callback) => {
      const [inputs, setInputs] = useState({
        username: '',
        password: '',
        email: '',
        full_name: '',
      });
    
      const handleInputChange = (name, text) => {
        console.log(name, text);
        setInputs((inputs) => {
          return {
            ...inputs,
            [name]: text,
          };
        });
      };
      return {
        handleInputChange,
        inputs,
      };
    };
    
    export default useSignUpForm;
    ```
4. Do the same with LoginForm.
   * Instead of using 'RegisterHooks.js' as filename, use 'LoginHooks.js'
   * Rename 'useSignUpForm' function in 'LoginHooks.js' to 'useLoginForm'
   * Make this change:
   ```javascript
   // LoginHooks.js:
   const [inputs, setInputs] = useState({
       username: '',
       password: '',
     });
   ```
    
5. In APiHooks.js create function 'register' with corresponding functionality. Log the results of API fetches to console at this point. Also move the login function from Login.js to APIhooks.js.
    * Example 'register' function:
    ```javascript
    const register = async (inputs) => {
      const fetchOptions = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(inputs),
      };
      try {
         const response = await fetch(apiUrl + 'users', fetchOptions);
         const json = await response.json();
         return json;
      } catch (e) {
          console.log('ApiHooks register', e.message);
          return false;
      }
    };
    ```
6. To prevent warnings about Promises use try/catch for all awaits. You can use one try for multiple awaits.
7. Use register function from APIhooks.js in _RegisterForm()_ function:
   ```jsx
   ...
   const doRegister = async () => {
       const serverResponse = await register(inputs);
       if (serverResponse) {
         Alert.alert(serverResponse.message);
       } else {
         Alert.alert('register failed');
       }
   };
   
   const {inputs, handleInputChange} = useSignUpForm(); // makes inputs and handleInput change visible from RegisterHooks.js
   ...
   ```
8. Do the login functionalites the same way as above to LoginForm.js
9. Add the final functionalities:
    * when logging in, save user data to [Context](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react). Save token to AsyncStorage. With Context you can create a global state which can be accessed from all components.
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
10. Try the app on a real device. You can see that it's hard/impossible to write since keyboard is covering the input fields. Use [KeyboardAvoidingView](https://reactnative.dev/docs/keyboardavoidingview) in Login.js to fix the issue. 
11. Use the saved user data in _Profile.js_
    - log user data to console (for debugging)
    - use [_Text_ component](https://reactnative.dev/docs/text) to display the user data on the profile page
12. Add and commit changes to git, push to Github/GitLab.
