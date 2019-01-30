class: center, middle

# WBMA, Forms

## 3/2019

---

# Forms

## Task 1: Smarter Login/Registration page

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Show only login form when opening the 'login-register' page
1. Add a link/button for switching between login/register forms ("No account yet?" or something).
    - use e.g. boolean variable to keep track of the state in the `.ts` file
1. When registering check that the username is free just after the username input field gets filled
    - use e.g. `ionBlur` event
    - show notification if username is already in use
1. Add "confirm password" functionality
   - add another password field
   - check that user input of both password fields match before api call
   - notify user if passwords do not match

## Task 2: Form validation

- User inputs should always be checked before making any api calls
  - username must exist and be long enough
  - password must exist and be long enough
  - email format must be correct
  - full name is optional but should be validated if entered?

1. Study [template driven forms](https://codecraft.tv/courses/angular/forms/template-driven/)
1. Add required input validation to each field
1. Notify the user about problems when needed
1. Reset the form after succesful submission

_Note:_ WBMA API update: new user registrations without valid username (min length 3 characters), password (min length 5) and email (correctly formatted) are not accepted anymore.

## Extra

- Add user update functionality to profile page
- check: <https://media.mw.metropolia.fi/wbma/docs/#api-User-PutUser>

---

### Learn about how Angular handles forms

- [Angular forms](https://angular.io/guide/forms)
- [Codecraft](https://codecraft.tv/courses/angular/forms/overview/)
- [Tutorial: Advanced Forms & Validation in Ionic 2 & 3](https://www.joshmorony.com/advanced-forms-validation-in-ionic-2/)