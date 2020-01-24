# Navigation

## 2/2019

---

# Routing 

Study:
* [Three dots](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
* [React Navigation](https://reactnavigation.org/docs/en/getting-started.html)
* [Stack Navigation](https://reactnavigation.org/docs/en/hello-react-navigation.html)
* [Tab Navigation](https://reactnavigation.org/docs/en/tab-based-navigation.html)
* Navigation prop reference, createStackNavigator, createBottomTabNavigator in the [API](https://reactnavigation.org/docs/en/api-reference.html)

#### A
1. Create a new react native project called 'Stack' with Expo CLI. Make this separate from the app we did in previous labs. No need to submit this or push it to Git
1. Install react-navigation with npm `npm install react-navigation --save`
1. Install react-navigation-stack with npm `npm install react-navigation-stack --save`
1. Install these packages with expo to get correct versions: `expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context`
1. Follow [Hello React Navigation](https://reactnavigation.org/docs/en/hello-react-navigation.html) and [Moving between screens](https://reactnavigation.org/docs/en/navigating.html) articles to create a simple stack navigation

#### B
1. Create a new react native project called 'Tabs' with Expo CLI. Make this separate from the app we did in previous labs. No need to submit this or push it to Git
1. Install react-navigation with npm `npm install react-navigation --save`
1. Install react-navigation-tabs with npm `npm install --save react-navigation-tabs`
1. Install these packages with expo to get correct versions: `expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context`
1. Follow [Tab Navigation](https://reactnavigation.org/docs/en/next/tab-based-navigation.html) article to create a simple tab navigation

#### C
Continue the app made in previous labs. Create a new branch `navigation` with git and checkout it (`git checkout -b navigation`).
1. Goal is to make a navigation between three 'pages'
    * Bottom tab menu has two links: 'Home' and 'Profile'
    * Each thumbnail is TouchableOpacity and tapping them should take to 'Single' to show the selected media file (just images at this point)
1. Install react-navigation with npm `npm install react-navigation --save`
1. Install react-navigation-tabs with npm `npm install --save react-navigation-tabs`
1. Install react-navigation-stack with npm `npm install react-navigation-stack --save`
1. Install these packages with expo to get correct versions: `expo install react-navigation react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view`
1. Create new folder 'views'
1. Create 'Home.js', 'Single.js' and 'Profile.js' to 'views'
1. Home.js will be the component that should show first when the app starts
    * Copy the content of App.js to Home.js and change function name and export default to Home
    * Modify Home function: 
    ```jsx harmony
      const Home = () => {
        return (
          <View style={styles.container}>
            <List></List>
          </View>
        );
      };

    ```
    * Modify App.js:
    ```jsx harmony
      const App = () => {
        return (
          <MediaProvider>
            <Home></Home>
          </MediaProvider>
        );
      };
    ``` 
    * Remove unused styles and imports etc.
    * The app should at this point work the same as before
1. Content for Profile.js
    ```jsx harmony
    import React from 'react';
    import {StyleSheet, View, Text} from 'react-native';
    
    const Profile = () => {
      return (
        <View style={styles.container}>
          <Text>Profile</Text>
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
    
    export default Profile;
    ```
1. Content for Single.js:
   ```jsx harmony
   import React from 'react';
   import {StyleSheet, View, Text} from 'react-native';
   
   const Single = () => {
     return (
       <View style={styles.container}>
         <Text>Single</Text>
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
   
   export default Single;
   ```

1. Create tab navigation
    * create new folder 'navigators'
    * create new file 'Navigator.js' to 'navigators'
    * in 'Navigator.js' use `createBottomTabNavigator` to make a simple tab navigation to Home and Profile 
    ```jsx harmony
    ...
    const Navigator = createBottomTabNavigator(
        {
          Home: {
            screen: Home,
            navigationOptions: {
              title: 'Home',
            },
          },
          Profile: {
            screen: Profile,
            navigationOptions: {
              title: 'Profile',
            },
          },
        },
        {
          initialRouteName: 'Home',
        }
    );
   ...
    ```
   * modify App.js (remember to add neccessary and remove unneccessary imports):
   ```jsx harmony
   const App = () => {
     return (
       <MediaProvider>
         <Navigator></Navigator>
       </MediaProvider>
     );
   };
   ```
    * The app should at this point have tab navigation between Home and Profile

#### D. Navigate to 'Single' component by tapping thumbnails
1. For this we need to combine tab navigation with stack navigation in Navigator.js:
    ```jsx harmony
    import {createAppContainer} from 'react-navigation';
    import {createBottomTabNavigator} from 'react-navigation-tabs';
    import {createStackNavigator} from 'react-navigation-stack';
    import Home from '../views/Home';
    import Profile from '../views/Profile';
    import Single from '../views/Single';
    
    const TabNavigator = createBottomTabNavigator(
        {
          Home: {
            screen: Home,
            navigationOptions: {
              title: 'Home',
            },
          },
          Profile: {
            screen: Profile,
            navigationOptions: {
              title: 'Profile',
            },
          },
        },
        {
          initialRouteName: 'Home',
        }
    );
    
    const Navigator = createStackNavigator(
        // RouteConfigs
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
        },
    );
    
    export default createAppContainer(Navigator);
    ```
    * If title in header is not changing, add the following code after TabNavigator function:
    ```javascript
    TabNavigator.navigationOptions = ({navigation}) => {
     const {routeName} = navigation.state.routes[navigation.state.index];

     // You can do whatever you like here to pick the title based on the route name
     const headerTitle = routeName;

     return {
       headerTitle,
     };
   };

    ```
1. Pass 'navigation' prop from Home to List to ListItem and use push-method to navigate to 'Single'-component:
   ```jsx harmony
   // Home.js
   const Home = (props) => {
      const {navigation} = props;
      return (
        <View style={styles.container}>
          <List navigation={navigation}></List>
        </View>
      );
   };
   
   // List.js
   const List = (props) => {
     ...
     return (
       <FlatList
         ...
         renderItem={
           ({item}) => <ListItem
             navigation={props.navigation}
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
             props.navigation.push('Single');
           }
         }
         ...
       >
    ``` 
1. The app should at this point navigate to 'Single' component when any thumbnail is tapped
  
#### E. Show selected file in 'Single' component
1. Study [Passing parameters to routes](https://reactnavigation.org/docs/en/params.html)
1. In 'ListItem' you have file data in props. Pass the file data as a parameter with navigation.push
1. In Single.js receive the file parameter and use it's 'filename' property to show the file in `<Image>` and 'title' property in `<Text>`
1. git add, commit & push to remote repository

#### F - Optional -
1. Study [Asynchronous image loading](https://snack.expo.io/HkjHS1ttZ)
1. Use `<AsyncImage>` instead of `<Image>` in the whole app to show text 'Loading' or [ActivityIndicator](https://docs.expo.io/versions/latest/react-native/activityindicator/)
 when images are loading

---

