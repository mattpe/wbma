class: center, middle

# WBMA, Ionic Routing

## 2/2019

---
# Routing

1. Continue last exercise. Create a new branch with git.
1. Create new pages 'register', 'login' and 'logout'
1. Create templates for 'login' and 'register' components yourself
1. Create tab navigation....
1. For routing edit X
___

# Using providers II - Login

1. In the MediaProcider create methods 'register' and 'login' with corresponding functionalities
 - 'login': call media API to login user and save users token to [local storage](http://www.w3schools.com/html/html5_webstorage.asp)
    - when logged in, user is redirected to 'front'
    - if user has already logged in redirect to 'front' (autodirect)
- 'register': call media API to create new user and automatically login
- [Forms with ngModel](https://ionicframework.com/docs/developer-resources/forms/)


---
# Some help

- [Tabs](https://ionicframework.com/docs/api/components/tabs/Tabs/#usage)
- [NavController](https://ionicframework.com/docs/api/navigation/NavController/)



# Google maps (optional task)
1. Create new page 'map' and add it to tabs
1. Follow [this tutorial](https://www.javascripttuts.com/implementing-native-google-maps-in-an-ionic-application/) to add Google Maps plugin to your app
1. iOS developers need [cocoaPods](https://cocoapods.org/app) and this [fix](https://ionic.zendesk.com/hc/en-us/articles/360010049673-Managing-plugins-using-cocoapods-in-Ionic-Pro)
1. API key can be found in Oma assignments