# Login, Register

## 2/2019

## Authentication

* Study:
  * [AsyncStorage](https://docs.expo.io/versions/latest/react-native/asyncstorage/#__next)
  * [React Navigation authentication flows](https://reactnavigation.org/docs/en/auth-flow.html)

### A. hard coded login

1. Continue last exercise. Create a new branch with git.
1. Create 'AuthLoading.js', 'Login.js' to 'views/'
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
      AsyncStorage,
    } from 'react-native';

   const Login = (props) => { // props is needed for navigation
     const signInAsync = async () => {
         await AsyncStorage.setItem('userToken', 'abc');
         props.navigation.navigate('App');
       };
      return (
        <View style={styles.container}>
          <Text>Login</Text>
          <Button title="Sign in!" onPress={
            () => {
              signInAsync(); 
            }
          } />
        </View>
      );
    };

    const styles = StyleSheet.create({
      container: {
        flex: 1,
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
        paddingTop: 40,
      },
    });

   // proptypes here

    export default Login;
   ```

1. _AuthLoading.js_:

   ```jsx harmony
   import React, {useEffect} from 'react';
   import {
     ActivityIndicator,
     AsyncStorage,
     StatusBar,
     View,
     Text,
   } from 'react-native';

   const bootstrapAsync = async (props) => {
     const getToken = async () => {
       const userToken = await AsyncStorage.getItem('userToken');

       // This will switch to the App screen or Auth screen and this loading
       // screen will be unmounted and thrown away.
       console.log('token', userToken);
       props.navigation.navigate(userToken ? 'App' : 'Auth');
     }
     useEffect(() => {
       getToken();
     }, []);
   };

   const AuthLoading = (props) => {
     bootstrapAsync(props);
     return (
       <View>
         <ActivityIndicator />
         <StatusBar barStyle="default" />
       </View>
     );
   };

   export default AuthLoading;
   ```

1. Modify _Navigator.js_ to add switch navigator like in [Authentication flows](https://reactnavigation.org/docs/en/auth-flow.html):

    ```jsx harmony
   ...
   import AuthLoading from '../views/AuthLoading';
   import Login from '../views/Login';
   ...
   const StackNavigator = createStackNavigator(
        {
          Home: {
            screen: TabNavigator,
            navigationOptions: {
              headerMode: 'none', // this will hide the header
            },
          },
          Single: {
            screen: Single,
          },
          Logout: {
            screen: Login,
          },
        },
    );
  
    const Navigator = createSwitchNavigator(
        {
          AuthLoading: AuthLoading,
          App: StackNavigator,
          Auth: Login,
        },
        {
          initialRouteName: 'AuthLoading',
        }
    );
    ...
   ```
  
1. Logout functionality to _Profile.js_:

   ```jsx harmony
   ...

   const Profile = (props) => {
     const signOutAsync = async () => {
          await AsyncStorage.clear();
          props.navigation.navigate('Auth');
        };
     return (
       <View style={styles.container}>
         <Text>Profile</Text>
         <Button title="Logout!" onPress={signOutAsync} />
       </View>
     );
   };
   ...
   ```

1. At this point the app should have basic login/logout functionality.

### B. Fetch token from Media API

1. Recap how to make [POST request with fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Supplying_request_options)
1. [Login endpoint in the Media API](http://media.mw.metropolia.fi/wbma/docs/#api-Authentication-PostAuth)
1. Modify _Login.js_

   ```jsx harmony
   ...
   const signInAsync = async (props) => {
     // do async fetch here like in List and ListItem
     // hard code your username and password
     // you need to use POST method, see API documentation for details
     await AsyncStorage.setItem('userToken', tokenFromApi);
     props.navigation.navigate('App');
   };
   ...
   ```

### C. Login form

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
      * note that article is React (HTML) but we are coding React Native, for example the [events](https://facebook.github.io/react-native/docs/textinput#onchangetext) are different.
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
   * Modify 'signInAsync' function to get username and password from 'inputs' object

1. Display user's info (username, fullname and email) in _Profile.js_
   * You can store also the user data to AsyncStorage
   * Remember that AsyncStorage is asynchronous, so you need useState-hook to display anything stored to AsyncStorage and useEffect-hook to prevent infinite loop.

### D. Registering

1. Add another "form" to _Login.js_ for registering.
   * registering is basically the same as login. The difference is the [endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-PostUser) in the media API
1. Do the registering functionality the same way as login functionality
1. Make login to happen automatically after registering
   * in other words run 'signInAsync' after registering is done

### Extra. Optimize APIHooks.js

1. Don't repeat yourself! Is there any repeating code in APIHooks.js that you could put into a separate function? 
