# WBMA, First App

## 1/2020

---

## Exercise 1: Setup your toolchain and create a new React Native project

Study [Getting started and Learn the basics](https://facebook.github.io/react-native/docs/getting-started) from React Native documentation

**a.**

1. If needed, install code editor (+ extensions), git, npm
1. Use the [expo](https://docs.expo.io/versions/v36.0.0/get-started/create-a-new-app/) cli tool to generate an app skeleton
    * create a folder for your React Native projects
    * use Git Bash or terminal to go to this folder `cd foldername/otherfoldername/etc...`
    * `npm install -g expo-cli`
    * `expo init MyApp`
        * choose 'blank' template
        * if this fails on Windows due to missing interactive mode, use cmd instead of Git Bash
1. Test that app works; run it and open in browser (interactive shell is needed to get the menu option (_w_) for launhing in browser)
    * `cd MyApp`
    * `npm start`
1. Create a remote git repository (Github) and push your app there

**b.**

1. Install ESlint to your project `npm i --save-dev eslint eslint-plugin-react eslint-plugin-react-native babel-eslint`
1. Initialize ESlint: `./node_modules/.bin/eslint --init` or `node node_modules\eslint\bin\eslint.js --init` (note: needs an interactive shell and does not work in Git Bash on Windows. Use cmd or VSCode's terminal instead.)
    * Choose:
        1. To check syntax, find problems, and enforce code style
        1. JavaScript modules (import/export)
        1. React
        1. No TypeScript
        1. Browser
        1. Use a popular style guide
        1. Google
        1. JavaScript
        1. Y
1. Modify .eslintrc.js:

   ```JavaScript
    module.exports = {
      'parser': 'babel-eslint',
      'env': {
        'browser': true,
        'es6': true,
      },
      'extends': [
        'google',
        'eslint:recommended',
        'plugin:react/recommended',
      ],
      'globals': {
        'Atomics': 'readonly',
        'SharedArrayBuffer': 'readonly',
      },
      'parserOptions': {
        'ecmaFeatures': {
          'jsx': true,
        },
        'ecmaVersion': 2018,
        'sourceType': 'module',
      },
      'plugins': [
        'react',
        'react-native'
      ],
      'rules': {
        'react/jsx-uses-react': 'error',
            'react/jsx-uses-vars': 'error',
            'no-console': 0,
            'require-jsdoc': 0,
      },
      'settings': {
        'react': {
          'createClass': 'createReactClass', // Regex for Component Factory to use,
                                             // default to "createReactClass"
          'pragma': 'React',  // Pragma to use, default to "React"
          'version': 'detect', // React version. "detect" automatically picks the version you have installed.
                               // You can also use `16.0`, `16.3`, etc, if you want to override the detected value.
                               // default to latest and warns if missing
                               // It will default to "detect" in the future
          'flowVersion': '0.53', // Flow version
        },
        'propWrapperFunctions': [
          // The names of any function used to wrap propTypes, e.g. `forbidExtraProps`. If this isn't set, any propTypes wrapped in a function will be skipped.
          'forbidExtraProps',
          {'property': 'freeze', 'object': 'Object'},
          {'property': 'myFavoriteWrapper'},
        ],
        'linkComponents': [
          // Components used as alternatives to <a> for linking, eg. <Link to={ url } />
          'Hyperlink',
          {'name': 'Link', 'linkAttribute': 'to'},
        ],
      },
    };
   ```

1. Create new file '.editorconfig' and add this content:

    ```editorconfig
    root = true

    [*]
    indent_style = space
    indent_size = 2
    end_of_line = lf
    charset = utf-8
    trim_trailing_whitespace = true
    insert_final_newline = true
    ```

1. You can format code automatically with _shift-alt-f_
1. Fix curly-braces error in Preferences/Settings
    * search for 'braces' and uncheck all 'Insert space after...' checkboxes
1. Convert the App function to arrow function:

    ```jsx harmony
   import React from 'react';
   import {StyleSheet, Text, View} from 'react-native';

   const App = () => {
     return (
       <View style={styles.container}>
         <Text>Open up App.js to start working on your app!</Text>
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

   export default App;
   ```

**c.**

1. Study [Handling Touches](https://facebook.github.io/react-native/docs/handling-touches) and [Using List Views](https://facebook.github.io/react-native/docs/using-a-listview)
1. Develop your app further. Add this after the import statements:

    ```ecmascript 6
    const mediaArray = [
      {
        'key': '0',
        'title': 'Title 1',
        'description': 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis sodales enim eget leo condimentum vulputate. Sed lacinia consectetur fermentum. Vestibulum lobortis purus id nisi mattis posuere. Praesent sagittis justo quis nibh ullamcorper, eget elementum lorem consectetur. Pellentesque eu consequat justo, eu sodales eros.',
        'thumbnails': {
          w160: 'http://placekitten.com/160/161',
        },
        'filename': 'http://placekitten.com/2048/1920',
      },
      {
        'key': '1',
        'title': 'Title 2',
        'description': 'Donec dignissim tincidunt nisl, non scelerisque massa pharetra ut. Sed vel velit ante. Aenean quis viverra magna. Praesent eget cursus urna. Ut rhoncus interdum dolor non tincidunt. Sed vehicula consequat facilisis. Pellentesque pulvinar sem nisl, ac vestibulum erat rhoncus id. Vestibulum tincidunt sapien eu ipsum tincidunt pulvinar. ',
        'thumbnails': {
          w160: 'http://placekitten.com/160/162',
        },
        'filename': 'http://placekitten.com/2041/1922',
      },
      {
        'key': '2',
        'title': 'Title 3',
        'description': 'Phasellus imperdiet nunc tincidunt molestie vestibulum. Donec dictum suscipit nibh. Sed vel velit ante. Aenean quis viverra magna. Praesent eget cursus urna. Ut rhoncus interdum dolor non tincidunt. Sed vehicula consequat facilisis. Pellentesque pulvinar sem nisl, ac vestibulum erat rhoncus id. ',
        'thumbnails': {
          w160: 'http://placekitten.com/160/163',
        },
        'filename': 'http://placekitten.com/2039/1920',
      },
    ];
    ```

1. Add `<Flatlist>`, `<TouchableOpacity>`, `<Text>` and `<Image>` components to the existing `<View>`. Example:

    ```jsx harmony
    <FlatList
        data={mediaArray}
        renderItem={({item}) => {
          return (
            <TouchableOpacity>
              <Image
                style={{width: 100, height: 100}}
                source={{uri: item.thumbnails.w160}}
              />
              <View>
                <Text>{item.title}</Text>
                <Text>{item.description}</Text>
              </View>
            </TouchableOpacity>
          );
        }}
      />
    ```

**d.**

1. Study [Layout with Flexbox](https://facebook.github.io/react-native/docs/flexbox)
1. Develop your app further. Modify the app so that the layout is similar to this:
    ![View 1](images/app01.png)
1. You can modify the styles either inline or by adding properties to the 'styles' object at the end of the file.

**e.**

1. Study [Props](https://facebook.github.io/react-native/docs/props) and [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)
1. Split the app to multiple files. In other words: create components.
    * Create a folder 'components' and there a new files 'List.js' and 'ListItem.js'
    * Component hierarchy:

    ```text
    App
       -View
           -List
               -ListItem
               ...

    ```

    * Move `<Flatlist>` to 'List.js' and the content of `<Flatlist>` to 'ListItem.js'
    * Add imports, component function and style object. (Basically the same as 'App.js'. Just change the name of the component function.)
    * PropTypes for List:

    ```jsx harmony
   List.propTypes = {
     mediaArray: PropTypes.array,
   };
   ```

    * PropTypes for ListItem:

   ```jsx harmony
    ListItem.propTypes = {
      singleMedia: PropTypes.object,
    };
    ```

    * In 'App.js' pass 'data' array as prop called 'mediaArray' from App to List:

    ```jsx harmony
    const App = () => {
      return (
        <View>
          <List mediaArray={mediaArray} />
        </View>
      );
    };
    ```

   * In 'List.js' pass 'item' object as prop called 'singleMedia' from List to ListItem:

   ```jsx harmony
    const List = (props) => {
      console.log(props);
      return (
        <FlatList
          data={props.mediaArray}
          renderItem={({item}) => <ListItem singleMedia={item} />}
        />
      );
    };
    ```

1. Create a new branch, add, commit & push your project to remote repository
    * `git checkout -b someBranchName`
    * `git add .`
    * `git commit -m "describe changes somehow"`
    * `git push`

---

### Bonus (Optional)

Develop your app further. Open 'filename' image in a [Modal](https://facebook.github.io/react-native/docs/modal.html) when `<TouchableOpacity>` is tapped.
