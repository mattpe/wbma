class: center, middle

# WBMA, Ionic Navigation

## 2/2019

---

# Navigation

1. Continue last exercise. Create a new branch with git.
1. Create new pages 'menu', 'login-register' and 'logout' (`ionic generate page <PageName> --no-module`)
1. Create templates for 'login-register' pages yourself
1. Create tab-navigation. Edit 'Menu'-page to add tab navigation.

## Some help

- [Tabs](https://ionicframework.com/docs/v3/api/components/tabs/Tabs/#usage)
- [NavController](https://ionicframework.com/docs/v3/api/navigation/NavController/)

---

# Using providers II - Login

1. In the MediaProvider create methods 'register' and 'login' with corresponding functionalities
 - 'login'-page: call media API to login user and save users token to [local storage](http://www.w3schools.com/html/html5_webstorage.asp)
    - when logged in, user is redirected to 'home'
    - if user has already logged in redirect to 'home' (autoredirect)
- 'register'-page: call media API to create new user 
    - login automatically after registering
    - check if username already exists
- [Forms with ngModel](https://ionicframework.com/docs/v3/developer-resources/forms/)
- 'logout'-page: logout
- Use [show]-attribute to show/hide login/logout buttons in tab-navigation according to user's login status


---

