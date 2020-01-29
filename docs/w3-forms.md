# WBMA, Forms

## 3/2019

---

## Forms

### Task 1: Smarter Login/Registration page

1. Study [Conditional rendering](https://reactjs.org/docs/conditional-rendering.html)
    * especially [Inline If with Logical && Operator](https://reactjs.org/docs/conditional-rendering.html#inline-if-with-logical--operator)
1. Continue the previous exercise. Create a new git branch for these tasks.
1. Show only login form when opening the Login page
   * remember that changing the view requires change in state (useState)
1. Add a link/button for switching between login/register forms ("No account yet?" or something).
1. When registering check that the username is free just after the username input field gets filled
   * there is an [endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-CheckUserName) for that
   * use e.g. [onChangeText](https://facebook.github.io/react-native/docs/textinput.html#onchangetext)  or [onEndEditing](https://facebook.github.io/react-native/docs/textinput.html#onendediting) events

   ```jsx harmony
   <TextInput
   onEndEditing={(evt) =>
        {
            const text = evt.nativeEvent.text;
        }
     }
   />
   ```

   * show notification if username is already in use

### Task 2: Form validation

* Study [Validating Forms in React Native](https://medium.com/@pavsidhu/validating-forms-in-react-native-7adc625c49cf) and [Validate.JS](http://validatejs.org/)
* User inputs should always be checked before making any api calls
  * username must exist and be long enough (see below)
  * password must exist and be long enough (see below)
  * email format must be correct
  * full name is optional but should be validated if entered(?)

1. Add "confirm password" functionality
    * add another password field
    * check that user input of both password fields match before making an api call
    * notify user if the passwords do not match
1. Add required input validation to each field
1. Notify the user about problems when needed
1. You can also combine username availability with the rest of the form validation

_Note:_ new user registrations without valid username (min length 3 characters), password (min length 5) and email (correctly formatted) are not accepted

### Extra

* Add user update functionality to profile page
* Check: <https://media.mw.metropolia.fi/wbma/docs/#api-User-PutUser>
