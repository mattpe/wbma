# Login, Register

## 2/2019

## Authentication

* Study:
  * [React Navigation authentication flows](https://reactnavigation.org/docs/auth-flow/)
  * [Context](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
  * [AsyncStorage](https://react-native-community.github.io/async-storage/docs/usage/)
                                                                                       
### A. hard coded login

1. Continue last exercise. Create a new branch with git.
1. Create 'Login.js' to 'views/'
1. _Login.js_
    * Eventually this will be the login and register page
    * For now we'll do hard coded login:

    ```jsx harmony
    import React from 'react';
    import {
      StyleSheet,
      View,
      Text,
      Button,
    } from 'react-native';
    import PropTypes from 'prop-types';   
    
    const Login = (props) => { // props is needed for navigation   
      const logIn = () => {
          props.navigation.navigate('Home');
      };
      return (
        <View style={styles.container}>
          <Text>Login</Text>
          <Button title="Sign in!" onPress={logIn}/>
        </View>
      );
    };
    
    const styles = StyleSheet.create({
      container: {
        flex: 1,
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
      },
    });
    
    Login.propTypes = {
      navigation: PropTypes.object,
    };
    
    export default Login;

   ```

1. Modify _Navigator.js_ to add conditional navigator like in [Authentication flows](https://reactnavigation.org/docs/auth-flow/):

   ```jsx harmony
   ...
   const StackScreen = () => {
     const isLoggedIn = false;
     return (
       <Stack.Navigator>
         {isLoggedIn ? (
           <>
             <Stack.Screen name="Home" component={TabScreen}/>
             <Stack.Screen name="Single" component={Single}/>
           </>
         ) : (
           <>
             <Stack.Screen name="Login" component={Login}/>
           </>
         )}
       </Stack.Navigator>
     );
   };
   ...
   ```

1. At this point you should see Login screen when you start the app. If you change the value of isLoggedIn to true you should see the Home page

### B. Context
1. To do actual login/logout we need to add a [context](https://reactjs.org/docs/context.html) to change the value of isLoggedIn and to share that to different components like Navigator, Login and Profile
1. Create folder 'contexts' and there add a new file 'AuthContext.js':
   ```jsx
   import React, {useState} from 'react';
   import PropTypes from 'prop-types';
   
   const AuthContext = React.createContext({});
   
   const AuthProvider = (props) => {
     const [isLoggedIn, setIsLoggedIn] = useState(false);
   
     return (
       <AuthContext.Provider value={[isLoggedIn, setIsLoggedIn]}>
         {props.children}
       </AuthContext.Provider>
     );
   };
   
   AuthProvider.propTypes = {
     children: PropTypes.node,
   };
   
   export {AuthContext, AuthProvider};
   ```
1. Add AuthProvider to App.js so components can access the context
   ```jsx
   ...
    <AuthProvider>
         <Navigator/>   
   </AuthProvider>
   ...
   ```
1. Modify Navigator.js to use AuthContext:
   ```jsx
   ...
   const StackScreen = () => {
     const [isLoggedIn] = useContext(AuthContext);
   ...
   ```
1. Modify Login.js to use AuthContext:
   ```jsx
   ...
   const Login = (props) => { // props is needed for navigation
     const [isLoggedIn, setIsLoggedIn] = useContext(AuthContext);
     console.log('ili', isLoggedIn);
     const logIn = () => {
       setIsLoggedIn(true);
       if (isLoggedIn) {  // this is to make sure isLoggedIn has changed, will be removed later
         props.navigation.navigate('Home');
       }
     };
     return (
   ...
   ```
1. Add logout functionality to _Profile.js_:
   ```jsx harmony
   ...
   const Profile = (props) => {
     const [isLoggedIn, setIsLoggedIn] = useContext(AuthContext);
     console.log('profile', isLoggedIn);
     const logout = () => {
       setIsLoggedIn(false);
       if (!isLoggedIn) { // this is to make sure isLoggedIn has changed, will be removed later
         props.navigation.navigate('Login');
       }
     };
     return (
       <SafeAreaView style={styles.container}>
         <Text>Profile</Text>
         <Button title={'Logout'} onPress={logout} />
       </SafeAreaView>
     );
   };
   ...
   ```
1. Remember to add necessary imports and PropTypes to above steps.
1. At this point the app should have basic login/logout functionality.

### C. Remembering if user has logged in
1. Install [AsyncStorage](https://react-native-community.github.io/async-storage/): `npm i @react-native-community/async-storage`
1. Import AsyncStorage to Login.js and Profile.js:
   ```jsx
   ...
   import AsyncStorage from '@react-native-community/async-storage';
   ... 
   ```
1. Modify logIn() function in Login.js:
   ```jsx
   const logIn = async () => {
      setIsLoggedIn(true);   
      await AsyncStorage.setItem('userToken', 'abc');
      props.navigation.navigate('Home');
     };
   ```
1. Modify logout() function in Profile.js:
   ```jsx
   const logout = async () => {
       setIsLoggedIn(false);
       await AsyncStorage.clear();
       props.navigation.navigate('Login');
     };
   ```
1. Add getToken() function to Login.js to check the token when app starts:
   ```jsx
   const getToken = async () => {
       const userToken = await AsyncStorage.getItem('userToken');
       console.log('token', userToken);
       if (userToken === 'abc') {
         setIsLoggedIn(true);
         props.navigation.navigate('Home');
       }
     };
     useEffect(() => {
       getToken();
     }, []);
   ```
1. Remeber to add necessary imports.
1. Press login and reload the app. App should go automatically to Home.
1. Logout and reload the app. App should stay in the Login screen.

### D. Fetch token from Media API

1. Recap how to make [POST request with fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Supplying_request_options)
1. [Login endpoint in the Media API](http://media.mw.metropolia.fi/wbma/docs/#api-Authentication-PostAuth)
1. Modify _logIn()_ function in _Login.js_. The function should get the token from the API

   ```jsx harmony
   ...
   const logIn = async () => {
     // do async fetch here like in List and ListItem
     // hard code your username and password
     // you need to use POST method, see API documentation for details
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


### D. Login form

1. Add 'FormTextInput.js' to 'components' folder:

   ```jsx harmony
   import React from 'react';
   import {StyleSheet, TextInput} from 'react-native';
   import PropTypes from 'prop-types';


   const FormTextInput = (props) => {
     const {style, ...otherProps} = props;
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

   FormTextInput.propTypes = {
     style: PropTypes.object,
   };

   export default FormTextInput;
   ```

1. Add two FormTextInputs to _Login.js_:

   ```jsx harmony
   ...
   return (
        <View style={styles.container}>
          <Text>Login</Text>
          <View style={styles.form}>
            <FormTextInput
              autoCapitalize='none'
              placeholder='username'
            />
            <FormTextInput
              autoCapitalize='none'
              placeholder='password'
              secureTextEntry={true}
            />
            <Button title="Sign in!" onPress={signInAsync} />
          </View>
        </View>
      );
   ...
   ```

1. Now we need to send the values from FormTextInputs to the API
   * study [this article about forms and hooks](https://medium.com/@geeky_writer_/using-react-hooks-to-create-awesome-forms-6f846a4ce57)
      * especially 'Creating Custom Hooks' and 'Connecting the Hook to the Form
      * note that article is React (HTML) but we are coding React Native, so for example the [events](https://facebook.github.io/react-native/docs/textinput#onchangetext) are different.
1. To get text from the form to local state, create 'LoginHooks.js' to 'hooks' folder
   * _LoginHooks.js_:

   ```jsx harmony
   import {useState} from 'react';

   const useSignUpForm = () => {
     const [inputs, setInputs] = useState({});
     const handleUsernameChange = (text) => {
       setInputs((inputs) =>
         ({
           ...inputs,
           username: text,
         }));
     };
     const handlePasswordChange = (text) => {
       setInputs((inputs) =>
         ({
           ...inputs,
           password: text,
         }));
     };
     return {
       handleUsernameChange,
       handlePasswordChange,
       inputs,
     };
   };

   export default useSignUpForm;
   ```

1. Modify _Login.js_
   * Add value and onChangeText attributes to FormTextInputs like in the linked article above
   * Modify _logIn()_ function to get username and password from 'inputs' object

1. Display user's info (username, fullname and email) in _Profile.js_
   * You can store also the user data to AuthContext
   
### D. Registering

1. Add another "form" to _Login.js_ for registering.
   * registering is basically the same as login. The difference is the [endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-PostUser) in the media API
1. Do the registering functionality the same way as login functionality
1. Make login to happen automatically after registering
   * in other words run _logIn()_ after registering is done

### Extra. Optimize APIHooks.js

1. Don't repeat yourself! Is there any repeating code in APIHooks.js that you could put into a separate function? 
