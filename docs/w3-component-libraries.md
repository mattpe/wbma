class: center, middle

# Component libraries

## 3/2020

---
There are many component libraries for React Native: [article 1](https://www.codeinwp.com/blog/react-native-component-libraries/), [article 2](https://blog.logrocket.com/react-native-component-libraries-in-2020/). In the classes we will be using [React Native Elements](https://reactnativeelements.com/). Feel free to use some other library if you want.
### Setup

1. Continue last exercise. Create a new branch 'comp-lib' with git.  
2. Study [getting started](https://reactnativeelements.com/docs/)
3. Install React Native Elements
    - `npm i react-native-elements`
4. Note: Remove all styling from the files where you use React Native Elements components:

   ```jsx harmony
   // remove this part:
   const styles = StyleSheet.create(...
   ```

    - You can customise React Native Elements components later
5. [React Native Elements components](https://reactnativeelements.com/docs/overview)
   - Some components you may find useful for the task: `Button`, `Card`, `Divider`, `Content`, `Header`, `Icon`, `Text`...    
   - By default [Icon component](https://reactnativeelements.com/docs/icon) uses  [Material icons](https://material.io/resources/icons/?style=baseline) as value for type attribute
6. In our app there is already `ListItem` component so if you want to use the [ListItem](https://reactnativeelements.com/docs/listitem) component of React Native Elements you need to use `import as` syntax:

   ```jsx harmony
   ...
   import {ListItem as NBListItem} from 'react-native-elements';
   ...
   return (
         <NBListItem thumbnail>
               <Left>
                 <Thumbnail>
         etc...
     );
   ```

7. [Adding icons to bottom tabs](https://reactnavigation.org/docs/material-bottom-tab-navigator/#example)


### Task A: Develop profile page

1. Add avatar/profile image to the user
    - Use postman to upload image and add a [tag](http://media.mw.metropolia.fi/wbma/docs/#api-Tag-PostTag) 'avatar_CurrentUserId' to it (e.g avatar_85)
    - When fetching avatars, you can use _CurrentUserId to limit the amount of fetched data.
2. Display users avatar image, name and email in profile page
   - You'll need to use existing or add more functions to 'ApiHooks.js' to achieve this
   - You'll also need to add a new state to show the avatar after it's url has been loaded from the API:
   ```jsx
   // Profile.js
   ...
   const [avatar, setAvatar] = useState('http://placekitten.com/640'); // placekitten... is default is user has no avatar
   ...
   ```

   ![Profile screen](images/profile.png)

### Task B: Convert the app we've made so far to use React Native Elements

1. Try to make the app look something like these images:

   ![Login screen](images/login.png)

   ![Home screen](images/home.png)

   ![Single screen](images/single.png)

2. Tips'n tricks:
   1. [Adding SVG support](https://kumar2396jayant.medium.com/how-to-use-svg-in-react-native-e581eca59534)
   2. [Lottie](https://airbnb.design/lottie/)
      1. [Create Lottie without After Effects](https://www.youtube.com/watch?v=zoBMb72UDeI)
      2. [Convert SVG to Lottie](https://lottiefiles.com/svg-to-lottie/convert)
         1. [MacOS download](https://github.com/HaikuTeam/animator/releases/)
         2. Build with Windows
            1. [Step 1](https://github.com/HaikuTeam/animator#windows-os-dependencies) (no need for git or node installation, you have them already)
            2. [Step 2](https://github.com/HaikuTeam/animator#2-install-project-dependencies)
            3. [Step 3](https://github.com/HaikuTeam/animator#3-start-development-server)
   3. [Masonry list](https://github.com/hyochan/react-native-masonry-list#react-native-masonry-list)
3. Add and commit changes to git, push to Github/GitLab.

  
