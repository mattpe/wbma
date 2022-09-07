# Form validation

## Smarter forms
* Study Regular Expressions: [Learn Regular Expressions In 20 Minutes, Youtube](https://www.youtube.com/watch?v=rhzKDrUiJVk&t=588s), [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions), [some examples](https://devinduct.com/cheatsheet/10/regex)
* Study [Creating Form in React Native Using React Hook Form](https://medium.com/skyshidigital/creating-form-in-react-native-using-react-hook-form-a81a99e45605)


### Task 1: Smarter Login/Registration page

1. Continue the previous exercise. Create a new git branch 'smartforms' for these tasks.
1. Show only login form when opening the Login page
   * remember that updating the view requires change in state (useState)
1. Add a link/button for switching between login/register forms ("No account yet?" or something).
1. When registering check that the username is free just after the username input field gets filled
   * there is an [endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-CheckUserName) for that
     * add _checkUsername_ function to _useUser_ in ApiHooks.js. It should return true if username is available. If not, return false.
   * change the validation to happen when user leaves the input fields by adding `mode: 'onBlur'` to _useForm()_:
   * add _validate_ to _rules_ of `<Controller>` of username field
   ```jsx harmony
   <Controller
      ...
      rules={{
          required: true,
          validate: async (value) => {
            // TODO: call checkUsername, if username not available return 'Username is already taken' else return true 
          },
        }}
      ...
   />
   ```

   * show notification if username is already in use
      ```jsx
       // example using React Native Elements
          <Input
              onBlur={onBlur}
              onChangeText={onChange}
              value={value}
              autoCapitalize="none"
              placeholder="Username"
              errorMessage={errors.username && errors.username.message}
           />
      ```

### Task 2: Form validation

* Study [validation rules of React Hook Form](https://react-hook-form.com/api/useform/register)
* User inputs should always be checked before making any api calls
  * username must exist and be long enough (see below)
  * password must exist and be long enough (see below)
  * email format must be correct
  * full name is optional but should be validated if entered(?)

1. Add required input validation to each field
   ```jsx
   // required example
   rules={{
          required: {value: true, message: 'This is required.'},
   }}
   
   // minLength example
   rules={{
          minLength: {
            value: 8,
            message: 'X must be at least 8 characters',
          },
   }}
   
   // pattern example
   rules={{
          pattern: {
            value: /^[0-9]{5}$/,
            message: 'Not a postal code',
          },
   }}
   ``` 
2. Notify the user about problems by using the [_errorMessage_ prop of _Input_](https://reactnativeelements.com/docs/input#errormessage)
3. _Note:_ new user registrations without valid username, password and email are not accepted. Validation properties:
   1. username: required, at least 3 characters
   2. password: required, at least 5 characters
      1. Extra: at least one number and at least one capital letter of any language ([Study Unicode Categories](https://www.regular-expressions.info/unicode.html))
   3. email: required, correct format (use pattern for this)
   4. full_name: at least 3 characters
4. Add "confirm password" functionality
    * add another password field
    * check that user input of both password fields match before making an api call
    * notify user if the passwords do not match
    * you can do this by adding _validate_ to _rules_ of `<Controller>` of confirm password field
      * extract [_getValues_](https://react-hook-form.com/api/useform/getvalues) from _useForm_ to get the value of password field
    * before sending the form to the API you'll need to delete confirm password property from the data object because API will reject data if it has extra properties.

### Extra

* Add user update functionality to profile page
* Check: <https://media.mw.metropolia.fi/wbma/docs/#api-User-PutUser>
* Add user notifications for other errors too (network connection problems, failed login attempt, etc.)
