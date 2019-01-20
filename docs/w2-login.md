class: center, middle

# WBMA, Ionic Navigation

## 2/2019

---
# Navigation

1. Continue last exercise. Create a new branch with git.
1. Create new pages 'menu', 'login-register' and 'logout'
1. Create templates for 'login-register' components yourself
1. Create tab-navigation. Edit 'Menu'-page to add tab navigation.
## Some help

- [Tabs](https://ionicframework.com/docs/api/components/tabs/Tabs/#usage)
- [NavController](https://ionicframework.com/docs/api/navigation/NavController/)
___

# Using providers II - Login

1. In the MediaProcider create methods 'register' and 'login' with corresponding functionalities
 - 'login': call media API to login user and save users token to [local storage](http://www.w3schools.com/html/html5_webstorage.asp)
    - when logged in, user is redirected to 'home'
    - if user has already logged in redirect to 'home' (autodirect)
- 'register'-page: call media API to create new user 
    - login automatically after registering
    - check if username already exists
- [Forms with ngModel](https://ionicframework.com/docs/developer-resources/forms/)
- 'logout'-page: logout
- Use *ngIf to show/hide login/logout buttons in tab-navigation according to user's login status


---




# Google maps (optional task)
1. Create new page 'map' and add it to tabs
1. Follow [this tutorial](https://www.javascripttuts.com/implementing-native-google-maps-in-an-ionic-application/) to add Google Maps plugin to your app
1. iOS developers need [cocoaPods](https://cocoapods.org/app) and this [fix](https://ionic.zendesk.com/hc/en-us/articles/360010049673-Managing-plugins-using-cocoapods-in-Ionic-Pro)
1. API key can be found in Oma assignments