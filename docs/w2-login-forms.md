# Login and Register

1. Study [useState with forms](https://www.youtube.com/watch?v=R7T5GQLxRD4)
1. Study [Using React Hooks To Create Awesome Forms](https://medium.com/@geeky_writer_/using-react-hooks-to-create-awesome-forms-6f846a4ce57)
1. Continue last exercise. Create a new branch 'forms' with git.
### A. Fetch token from Media API

1. Recap how to make [POST request with fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Supplying_request_options)
1. [Login endpoint in the Media API](http://media.mw.metropolia.fi/wbma/docs/#api-Authentication-PostAuth)
1. Modify _logIn()_ function in _Login.js_. The function should get the token from the API

   ```jsx harmony
   ...
   const logIn = async () => {
     // do async fetch here like in List.js
     // hard code your username and password
     // you need to use POST method, see API documentation for details
     // handle errors with try/catch and response.ok
     await AsyncStorage.setItem('userToken', tokenFromApi);
     props.navigation.navigate('Home');
   };
   ...
   ```
1. Modify _getToken()_ function in _Login.js_. The function should check if _userToken_ matches the token fetched from the API and then allow or deny access to the app.
   ```jsx
   const getToken = async () => {
       const userToken = await AsyncStorage.getItem('userToken');
       console.log('token', userToken);
       // do async fetch to /users/user
       // you need to send userToken
       // if you get successful result 
       // set isLoggedIn to true
       // and navigate to Home
     };
   ```

### B. Login and Register forms  
 
1. Create files:
    * 'LoginHooks.js' and 'RegisterHooks.js' to 'hooks' 
    * 'LoginForm.js' and 'RegisterForm.js' to 'components'
1. Login.js will hold LoginForm and RegisterForm components
    * Add the usual imports, component function and export to LoginForm and RegisterForm
    * Modify Login.js:
    ```jsx harmony
    const Login = ({navigation}) => {
    ...   
    return (
        <View style={styles.container}>
          <Text>Login</Text>
          <LoginForm navigation={navigation}/>
          <RegisterForm navigation={navigation} />
        </View>
      );
   ...
   ```
1. Add form to RegisterForm.js with username, password, email and full_name fields and submit button:
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
    * Use 'CustomHooks.js' in 'Using React Hooks...' article as an example to handle form events. Instead of using 'CustomHooks.js' as filename, use 'RegisterHooks.js'
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
1. Do the same with LoginForm.
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
    
1. In APiHooks.js create function 'register' with corresponding functionality. Log the results of API fetches to console at this point. Also move the login function from Login.js to APIhooks.js.
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
      const response = await fetch(apiUrl + 'users', fetchOptions);
      const json = await response.json();
      console.log(json);
    };
    ```
1. To prevent warnings about Promises use try/catch for all awaits. You can use one try for multiple awaits.
1. Use register function from APIhooks.js in _RegisterForm()_ function:
   ```jsx
   ...
   const doRegister = async () => {
       try {
         const serverResponse = await register(inputs); // remember imports
         console.log(serverResponse);   
       } catch (e) {
         console.log(e.message);
       }
     };
   
   const {inputs, handleInputChange} = useSignUpForm(); // makes inputs and handleInput change visible from RegisterHooks.js
   ...
   ```
1. Do the login functionalites the same way as above to LoginForm.js
1. Make login to happen automatically after registering
   * in other words run _logIn()_ after registering is done
1. Add the final functionalities:
    * when logging in, save user data to [Context](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react). Save token to AsyncStorage. With Context you can create a global state which can be accessed from all components.
    * Modify AuthContext.js:
    ```jsx
    ...
    const AuthProvider = ({children}) => {
      const [isLoggedIn, setIsLoggedIn] = useState(false);
      const [user, setUser] = useState({});
    
      return (
        <AuthContext.Provider value={{isLoggedIn, setIsLoggedIn, user, setUser}}>
          {children}
        </AuthContext.Provider>
      );
    };
    ...
    ```
   * <b>Note the change from [] to {} in AuthContext.Provider value</b>. This means that you need to change square brackets to curly braces everywhere where you have `const [isLoggedIn, setIsLoggedIn] = useContext(AuthContext);`
   * Setting user data example:
   ```javascript
   // now the vars and funcs can be in any order.
   const {setUser, isLoggedIn, user, setIsLoggedIn} = useContext(authContext);
   setUser(userdataFromApi.user); 
   ```
1. Log the saved user data to console in Profile.js
1. Add and commit changes to git, push to Github/GItLab.
