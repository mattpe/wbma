class: center, middle

# NativeBase

## 3/2019

---
### Task A: Convert the app we've made so far to use NativeBase
1. Continue last exercise. Create a new branch with git.  
1. Study [this article](https://blog.bitsrc.io/11-react-native-component-libraries-you-should-know-in-2018-71d2a8e33312) and [NativeBase](https://nativebase.io/)
1. Convert the app we've made so far to use NativeBase
1. Install NativeBase
    - `npm install native-base --save`
    - `expo install expo-font`
1. Remove all styling from the files where you use NativeBase components:
   ```jsx harmony
   // remove this part:
   const styles = StyleSheet.create(...
   ```
    - You can customise NativeBase components later
1. [NativeBase components](https://docs.nativebase.io/Components.html#Components)
1. In our app there are already List and ListItem components so if you want to use the [List](https://docs.nativebase.io/Components.html#list-def-headref) component of NativeBase you need to use `import as` syntax:
   ```jsx harmony
   ...
   import {List as BaseList} from 'native-base';
   ...
   return (
       <Container>
         <BaseList
           dataArray={media}
           renderRow={
             (item) => <ListItem
               navigation={props.navigation}
               singleMedia={item}
             />
           }
           keyExtractor={(item, index) => index.toString()}
         />
       </Container>
     );
   ```
### Task B: Develop profile page
1. Add avatar image to the user
    - Use postman to upload image and add a tag 'avatar_SomeUserId' to it
1. Display users avatar image, name and email in profile page
   - You'll need to add more methods to 'ApiHooks.js' to achieve this
   - Hint: Userdata is already in AsyncStorage but it might be more convenient to add it also to context state:
   ```jsx harmony
   // MediaContext.js:
   import React, {useState} from 'react';
   import PropTypes from 'prop-types';
   
   const MediaContext = React.createContext({});
   const MediaProvider = (props) => {
     const {
       media: initialMedia,
       user: initialUser,
       children
     } = props;
     const [media, setMedia] = useState(initialMedia);
     const [user, setUser] = useState(initialUser);
   
     const appContext = {
       user,
       setUser,
       media,
       setMedia,
     };
   
     return (
       <MediaContext.Provider value={appContext}>
         {children}
       </MediaContext.Provider>
     );
   };
   
   MediaProvider.propTypes = {
     media: PropTypes.array,
     user: PropTypes.object,
     children: PropTypes.node,
   };
   
   MediaProvider.defaultProps = {
     media: [],
     selectedUser: {}
   };
   
   export {MediaContext, MediaProvider};

   
   // ApiHooks.js
   ...
   const userToContext = async () => { // Call this when app starts (= Home.js)
       const {user, setUser} = useContext(MediaContext);
       const getFromStorage = async () => {
         const storageUser = JSON.parse(await AsyncStorage.getItem('user'));
         console.log('storage', storageUser);
         setUser(storageUser);
       }
       useEffect(() => {
         getFromStorage();
       }, []);
       return [user];
     };
   ...
   
   // Home.js
   ...
   const Home = (props) => {
     ...
     const {userToContext} = mediaAPI();
     userToContext().then((user) => {
       console.log('usercontext', user);
     });
   ...
   ```


