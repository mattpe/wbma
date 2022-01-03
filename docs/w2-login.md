# Login (dummy)

## Authentication

* Study:
  * [Conditional rendering](https://reactjs.org/docs/conditional-rendering.html)
    * especially [Inline If with Logical && Operator](https://reactjs.org/docs/conditional-rendering.html#inline-if-with-logical--operator) and [Inline If-Else with Conditional Operator](https://reactjs.org/docs/conditional-rendering.html#inline-if-else-with-conditional-operator)
  * [React Navigation authentication flows](https://reactnavigation.org/docs/auth-flow/)
  * [Context](https://upmostly.com/tutorials/how-to-use-the-usecontext-hook-in-react)
  * [AsyncStorage](https://react-native-async-storage.github.io/async-storage/)
                                                                                       
### A. hard coded login

1. Continue last exercise. Create a new branch with git.
2. Create 'Login.js' to 'views/'
3. _Login.js_
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
    
    const Login = ({navigation}) => { // props is needed for navigation   
      const logIn = () => {
          console.log('Button pressed');
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

4. Modify _Navigator.js_ to add conditional navigator like in [Authentication flows](https://reactnavigation.org/docs/auth-flow/):

   ```jsx harmony
   ...
   const StackScreen = () => {
     const isLoggedIn = false;
     return (
       <Stack.Navigator>
         // TODO: if isLoggedIn is true render Home and Single      
             <Stack.Screen name="Home" component={TabScreen}/>
             <Stack.Screen name="Single" component={Single}/>          
         // TODO: else render Login
             <Stack.Screen name="Login" component={Login}/>          
       </Stack.Navigator>
     );
   };
   ...
   ```

5. Complete the TODOs by using conditional rendering
6. At this point you should see Login screen when you start the app. If you change the value of isLoggedIn to true you should see the Home page

### B. Context

1. To do actual login/logout we need to add a [context](https://reactjs.org/docs/context.html) to change the value of isLoggedIn and to share that to different components like Navigator, Login and Profile
2. Create folder 'contexts' and there add a new file 'MainContext.js':
   ```jsx
   import React from 'react';
   import PropTypes from 'prop-types';
   
   const MainContext = React.createContext({});
   
   const MainProvider = (props) => {
     // TODO: create state isLoggedIn, set value to false
   
     return (
       <MainContext.Provider value={[isLoggedIn, setIsLoggedIn]}>
         {props.children}
       </MainContext.Provider>
     );
   };
   
   MainProvider.propTypes = {
     children: PropTypes.node,
   };
   
   export {MainContext, MainProvider};
   ```
3. Complete the TODO
4. Add MainProvider to App.js so components can access the context
   ```jsx
   ...
    <MainProvider>
         <Navigator/>   
   </MainProvider>
   ...
   ```
5. Modify Navigator.js to use MainContext:
   ```jsx
   ...
   const StackScreen = () => {
     const [isLoggedIn] = useContext(MainContext);
   ...
   ```
6. Modify Login.js to use MainContext:
   ```jsx
   ...
   const Login = ({navigation}) => { // props is needed for navigation
     // TODO: get isLoggedIn and setIsLoggedIn from MainContext
     console.log('login isLoggedIn', isLoggedIn);
     const logIn = () => {
       // TODO: set isLoggedIn to true;
       // TODO: if isLoggedIn is true navigate to Home (this if statement is to make sure isLoggedIn has changed, will be removed later)
     };
     return (
   ...
   ```
7. Add logout functionality to _Profile.js_:
   ```jsx harmony
   ...
   const Profile = ({navigation}) => {
     // TODO: get isLoggedIn and setIsLoggedIn from MainContext
     console.log('profile isLoggedIn', isLoggedIn);
     const logout = () => {
       // TODO: set isLoggedIn to false;
       // TODO: if isLoggedIn is false navigate to Login (this if statement is to make sure isLoggedIn has changed, will be removed later)
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
8. Remember to add necessary imports and PropTypes to above steps.
9. At this point the app should have simple login/logout functionality.

### C. Remembering if user has logged in
1. Install [AsyncStorage](https://react-native-async-storage.github.io/async-storage/docs/install/): `npm i @react-native-async-storage/async-storage`
2. Import AsyncStorage to Login.js and Profile.js:
   ```jsx
   ...
   import AsyncStorage from '@react-native-async-storage/async-storage';
   ... 
   ```
3. Modify logIn() function in Login.js:
   ```jsx
   const logIn = async () => {
      setIsLoggedIn(true);   
      await AsyncStorage.setItem('userToken', 'abc');
      navigation.navigate('Home');
     };
   ```
4. Modify logout() function in Profile.js:
   ```jsx
   const logout = async () => {
       setIsLoggedIn(false);
       await AsyncStorage.clear();
       navigation.navigate('Login');
     };
   ```
5. Add getToken() function to Login.js to check the token when app starts:
   ```jsx
   const getToken = async () => {
       // TODO: save the value of userToken saved in AsyncStorage as userToken
       console.log('token', userToken);
       // TODO if the content of userToken is 'abc'), set isLoggedIn to true and navigate to Home
     };
     useEffect(() => {
       getToken();
     }, []);
   ```
6. Remeber to add necessary imports.
7. Press login and reload the app. App should go automatically to Home.
8. You will get warning 'Possible Unhandled promise rejection'. Fix it by adding try/catch to all promises (await ....)
9. Logout and reload the app. App should stay in the Login screen.
10. Add and commit changes to git, push to Github/GItLab.
