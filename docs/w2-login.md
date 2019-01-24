class: center, middle

# WBMA, Ionic Navigation

## 2/2019

---

_Note 24.1.2019:_ Ionic framework v4 [was published](https://blog.ionicframework.com/introducing-ionic-4-ionic-for-everyone/) yesterday and the docs changed. We are still using v3 for now and the documentation is still available at <https://ionicframework.com/docs/v3/>. If old doc links are broken you can fix them by adding `v3/` into the url after the `docs/` part.   

---

# Navigation

1. Continue last exercise. Create a new branch with git.
1. Create new pages 'menu', 'login-register' and 'logout' (`ionic generate page <PageName> --no-module`)
1. Create template for the 'login-register' page yourself
1. Create tab-navigation. Edit 'Menu'-page to add tab navigation. Update the 'rootPage' of the app.

## Some help

- [Tabs](https://ionicframework.com/docs/v3/api/components/tabs/Tabs/#usage)
- [NavController](https://ionicframework.com/docs/v3/api/navigation/NavController/)

---

# Using providers II - Login

1. In the MediaProvider create methods 'register', 'login' and 'checkIfUserExists' with corresponding functionalities
 - 'login'-page: call media API to login user and save user's token to [local storage](http://www.w3schools.com/html/html5_webstorage.asp)
    - when logged in, user is redirected to 'home'
    - if user has already logged in redirect to 'home' (autoredirect)
- 'register'-page: call media API to create new user 
    - login automatically after registering
    - check if username already exists before trying to register
- [Forms with ngModel](https://ionicframework.com/docs/v3/developer-resources/forms/)
- 'logout'-page: logout (clear localstorage, update loggedIn status in media provider)
    - Use a [lifecycle event](https://blog.ionicframework.com/navigating-lifecycle-events/) for automatic method calls
- Use [show]-attribute to show/hide login/logout buttons in tab-navigation according to user's login status


---

