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
1. Create folder 'contexts' and there add a new file 'MainContext.js':
   ```jsx
   import React, {useState} from 'react';
   import PropTypes from 'prop-types';
   
   const MainContext = React.createContext({});
   
   const AuthProvider = (props) => {
     const [isLoggedIn, setIsLoggedIn] = useState(false);
   
     return (
       <MainContext.Provider value={[isLoggedIn, setIsLoggedIn]}>
         {props.children}
       </MainContext.Provider>
     );
   };
   
   AuthProvider.propTypes = {
     children: PropTypes.node,
   };
   
   export {MainContext, AuthProvider};
   ```
1. Add AuthProvider to App.js so components can access the context
   ```jsx
   ...
    <AuthProvider>
         <Navigator/>   
   </AuthProvider>
   ...
   ```
1. Modify Navigator.js to use MainContext:
   ```jsx
   ...
   const StackScreen = () => {
     const [isLoggedIn] = useContext(MainContext);
   ...
   ```
1. Modify Login.js to use MainContext:
   ```jsx
   ...
   const Login = (props) => { // props is needed for navigation
     const [isLoggedIn, setIsLoggedIn] = useContext(MainContext);
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
     const [isLoggedIn, setIsLoggedIn] = useContext(MainContext);
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
1. Add and commit changes to git, push to Github/GItLab.
