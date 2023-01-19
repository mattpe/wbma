# Profile page & Component libraries

## Task A: Develop a user profile page

1. Continue last exercise. Merge it to _main_ branch and create a new development branch _user-profile_ with git.  
1. Add avatar/profile image to the user
    - Use postman to upload image and add a [tag](http://media.mw.metropolia.fi/wbma/docs/#api-Tag-PostTag) 'avatar_CurrentUserId' to it (e.g 'avatar_85')
    - When fetching avatars, you can use _CurrentUserId_ to limit the amount of fetched data.
1. Display users avatar image, name and email in _profile_ page
   - You'll need to use existing or add more functions to _ApiHooks.js_ to achieve this
   - You'll also need to add a new state to show the avatar after it's url has been loaded from the API:
   ```jsx
   // Profile.js
   ...
   const [avatar, setAvatar] = useState('http://placekitten.com/640'); // placekitten... is default if user has no avatar
   ...
   ```

   ![Profile screen](images/profile.png)

---

## Task B: Convert the app we've made so far to use React Native Elements

There are many component libraries for React Native: [article 1](https://www.codeinwp.com/blog/react-native-component-libraries/), [article 2](https://blog.logrocket.com/react-native-component-libraries-in-2020/). In the classes we will be using [React Native Elements](https://reactnativeelements.com/). Feel free to use some other library if you want.

### Setup

1. Merge it to _main_ branch and create a new development branch _comp-lib_ with git.  
1. Study [getting started](https://reactnativeelements.com/docs/)
1. Install React Native Elements
    - `npm install @rneui/themed @rneui/base`
1. Install Peer dependencies
    - `npm install react-native-safe-area-context`
3. Note: Remove all styling from the files where you use React Native Elements components:

   ```jsx harmony
   // remove this part:
   const styles = StyleSheet.create(...
   ```

    - You can customise React Native Elements components later
1. [React Native Elements components](https://reactnativeelements.com/docs)
   - Some components you may find useful for the task: `Button`, `Card`, `Divider`, `Content`, `Header`, `Icon`, `Text`...    
   - By default [Icon component](https://reactnativeelements.com/docs/components/icon) uses  [Material icons](https://material.io/resources/icons/?style=baseline) as value for type attribute
1. In our app there is already `ListItem` component so if you want to use the [ListItem](https://reactnativeelements.com/docs/components/listitem) component of React Native Elements you need to use `import as` syntax:

   ```jsx harmony
   ...
   import {ListItem as RNEListItem} from '@rneui/themed';
   ...
   return (
         <RNEListItem thumbnail>
               <Left>
                 <Thumbnail>
         etc...
     );
   ```

1. [Adding icons to bottom tabs](https://reactnavigation.org/docs/material-bottom-tab-navigator/#example)

1. Try to make the app look something like these images:

   ![Login screen](images/login.png)

   ![Home screen](images/home.png)

   ![Single screen](images/single.png)

1. Tips'n tricks:
   1. [Adding SVG support](https://kumar2396jayant.medium.com/how-to-use-svg-in-react-native-e581eca59534)
   1. [Lottie](https://airbnb.design/lottie/)
      1. [Create Lottie without After Effects](https://www.youtube.com/watch?v=zoBMb72UDeI)
         1. [MacOS download](https://github.com/HaikuTeam/animator/releases/)
         2. Build with Windows
            1. [Step 1](https://github.com/HaikuTeam/animator#windows-os-dependencies) (no need for git or node installation, you have them already)
            2. [Step 2](https://github.com/HaikuTeam/animator#2-install-project-dependencies)
            3. [Step 3](https://github.com/HaikuTeam/animator#3-start-development-server)
      2. [Convert SVG to Lottie](https://lottiefiles.com/svg-to-lottie/convert)
   1. [Masonry list](https://github.com/hyochan/react-native-masonry-list#react-native-masonry-list)
1. Add and commit changes to git, push to Github/GitLab.
