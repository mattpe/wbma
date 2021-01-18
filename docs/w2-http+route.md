# Navigation

## 2/2019

---

# Routing 

Study:
* [Three dots](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
* [React Navigation](https://reactnavigation.org/docs/getting-started/)
* [Stack Navigation](https://reactnavigation.org/docs/hello-react-navigation/)
* [Tab Navigation](https://reactnavigation.org/docs/tab-based-navigation/)
* API Reference: [Navigation prop reference](https://reactnavigation.org/docs/navigation-prop), [createStackNavigator](https://reactnavigation.org/docs/stack-navigator), [createBottomTabNavigator](https://reactnavigation.org/docs/bottom-tab-navigator) 

#### A
1. Create a new react native project called 'Stack' with Expo CLI. Make this separate from the app we did in previous labs. No need to submit this or push it to Git
1. Install react-navigation with npm `npm i @react-navigation/native`
1. Install react-navigation-stack with npm `npm i @react-navigation/stack`
1. Install these packages with expo to get correct versions: `expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view`
1. Follow [Hello React Navigation](https://reactnavigation.org/docs/hello-react-navigation/) and [Moving between screens](https://reactnavigation.org/docs/navigating/) articles to create a simple stack navigation

#### B
1. Create a new react native project called 'Tabs' with Expo CLI. Make this separate from the app we did in previous labs. No need to submit this or push it to Git
1. Install react-navigation with npm `npm i @react-navigation/native`
1. Install react-navigation-bottom-tabs with npm `npm i @react-navigation/bottom-tabs`
1. Install these packages with expo to get correct versions: `expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view`
1. Follow [Tab Navigation](https://reactnavigation.org/docs/tab-based-navigation/) article to create a simple tab navigation

#### C
Continue the app made in previous labs. Create a new branch `navigation` with git and checkout it (`git checkout -b navigation`).
1. Goal is to make a navigation between three 'pages'
    * Bottom tab menu has two links: 'Home' and 'Profile'
    * Each thumbnail is TouchableOpacity and tapping them should take to 'Single' to show the selected media file (just images at this point)
1. Install react-navigation with npm `npm i @react-navigation/native`
1. Install react-navigation-bottom-tabs with npm `npm i @react-navigation/bottom-tabs`
1. Install react-navigation-stack with npm `npm i @react-navigation/stack`
1. Install these packages with expo to get correct versions: `expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view`
1. Create new folder 'views'
1. Create 'Home.js', 'Single.js' and 'Profile.js' to 'views'
1. Home.js will be the component that should show first when the app starts
    * Copy the content of App.js to Home.js and change function name and export default to Home
    * Modify Home function: 
    ```jsx harmony
      const Home = () => {
        return (
          <SafeAreaView style={styles.container}>
            <List />
            <StatusBar style="auto"/>
          </SafeAreaView>
        );
      };

    ```
    * Modify App.js:
    ```jsx harmony
      const App = () => {
        return (
            <Home></Home>
        );
      };
    ``` 
    * Remove unused styles and imports etc.
    * The app should at this point work the same as before
1. Content for Profile.js
    ```jsx harmony
    import React from 'react';
    import {StyleSheet, SafeAreaView, Text} from 'react-native';
    
    const Profile = () => {
      return (
        <SafeAreaView style={styles.container}>
          <Text>Profile</Text>
        </SafeAreaView>
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
    
    export default Profile;
    ```
1. Content for Single.js:
   ```jsx harmony
   import React from 'react';
   import {StyleSheet, SafeAreaView, Text} from 'react-native';
   
   const Single = () => {
     return (
       <SafeAreaView style={styles.container}>
         <Text>Single</Text>
       </SafeAreaView>
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
   
   export default Single;
   ```

1. Create tab navigation
    * create new folder 'navigators'
    * create new file 'Navigator.js' to 'navigators'
    * in 'Navigator.js' use `createBottomTabNavigator` to make a simple tab navigation to Home and Profile 
    ```jsx harmony
    import React from 'react';
    import {createBottomTabNavigator} from '@react-navigation/bottom-tabs';
    import {NavigationContainer} from '@react-navigation/native';
    
    const Tab = createBottomTabNavigator();
   
    const Navigator = () => {
      return (
        <NavigationContainer>
          // TODO: Make tab navigator here
        </NavigationContainer>
      );
    };
    
    export default Navigator;
   
    ```
   * modify App.js (remember to add neccessary and remove unneccessary imports):
   ```jsx harmony
   const App = () => {
     return (
         <Navigator></Navigator>
     );
   };
   ```
    * The app should at this point have tab navigation between Home and Profile

#### D. Navigate to 'Single' component by tapping thumbnails
1. For this we need to combine tab navigation with stack navigation in Navigator.js:
    ```jsx harmony
    // TODO: add neccessary imports
    
   // add after createBottomTabNavigator
    const Stack = createStackNavigator();
   
   const TabScreen = () => {
     return (
       // TODO: move content of <NavigationContainer> here
     );
   };
   
   const StackScreen = () => {
     return (
       <Stack.Navigator>
         // TODO: make two stack screens:
         // 1st: name=Home, component=TabScreen
         // 2nd: name=Single, component=Single
       </Stack.Navigator>
     );
   };
   
   const Navigator = () => {
     return (
       <NavigationContainer>
         <StackScreen/>
       </NavigationContainer>
     );
   };
    
   export default Navigator;
    ```
    
    1. Pass 'navigation' prop from Home to List to ListItem and use navigate-method to navigate to 'Single'-component:
   ```jsx harmony
   // Home.js
   const Home = (props) => {
      const {navigation} = props;
      ...
          <List navigation={navigation}></List>
      ...
   };
   
   // List.js
   const List = (props) => {
     ...
     return (
       <FlatList
         ...
         renderItem={
           ({item}) => <ListItem
             navigation={props.navigation} // without destucturing
             singleMedia={item}
           />
         }
         ...
       />
     );
   };
   
   // ListItem.js
   <TouchableOpacity
         ...
         onPress={
           () => {
             props.navigation.navigate('Single');
           }
         }
         ...
       >
    ``` 
1. When using props, remember to add the appropriate PropTypes
1. The app should at this point navigate to 'Single' component when any thumbnail is tapped
1. Try props with destructuring. E.g. `const Home = ({navigation}) => {` etc...
  
#### E. Show selected file in 'Single' component
1. Study [Passing parameters to routes](https://reactnavigation.org/docs/params/)
1. In 'ListItem' you have file data in props (singleMedia). Pass the file data as a parameter with navigation.navigate
1. In Single.js receive the file parameter and use it's 'filename' property to show the file in `<Image>` and 'title' property in `<Text>`
1. git add, commit & push to remote repository

#### F - Optional -
1. Study [Asynchronous image loading](https://snack.expo.io/HkjHS1ttZ)
1. Use `<AsyncImage>` instead of `<Image>` in the whole app to show text 'Loading' or [ActivityIndicator](https://docs.expo.io/versions/latest/react-native/activityindicator/)
 when images are loading

---

