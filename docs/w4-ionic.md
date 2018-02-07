class: center, middle

# WBMA, Ionic Framework

## 2/2018

---

## [Ionic](https://ionicframework.com/docs/)

- uses Angular for application logic
- [UI component library](https://ionicframework.com/docs/components/)
- [icon collection](https://ionicframework.com/docs/ionicons/)
- native capabilities based on [Cordova](https://cordova.apache.org/)
- Note: Old Ionic v1 uses old AngularJS (version 1.x), DO NOT touch that one

### From "basic" Angular to Ionic

Main differences in Ionic compared to "native" Angular web apps:

- Ionic uses the concept of pages (in Angular everything is just components, in Ionic term "component" refers typically to ready-made [UI components](https://ionicframework.com/docs/components/))
- different routing system, [navigation](https://ionicframework.com/docs//components/#navigation)
- services are called providers
- has it's own [cli tool](https://ionicframework.com/docs/cli/commands.html) `ionic`
- native plugins for different mobile platforms (Cordova)
- build target is a native mobile app, web browser is used for development

---

## Task: Port your app to Ionic framework

Add the features of the previous exercices into an Ionic application:

- user registration & login
- media file listing (incl. thumbnail pipe)
- file upload
- media service

1. Install Ionic & Cordova globally: `npm install -g cordova ionic`
1. Create a new Ionic app: `ionic start <APPNAME> <TEMPLATE>`
    - choose a starter template, [list of available options](https://ionicframework.com/docs/cli/starters.html#ionic-angular)
    - go with tabs/sidemenu template if you want to have some ready made examples of pages and navigation between them
    - note: we dont't use ionic1
1. Use Ionic cli to generate pages, `ionic generate page <NAME>`
    - front/home page for media (thumbnail) list view
    - user profile/login/registration pages
    - file upload page
1. Generate media provider (service), `ionic generate provider media`
1. Develop & test on browser: `ionic serve`
1. Run & test on mobile device
    - native mobile dev kit is needed, Xcode for iOS or Android SDK for Android
    - add your target platform: `ionic cordova platform add android/ios`
    - connect your device (USB)
    - install & start the app: `ionic cordova run android/ios`

---

### Some docs & tutorials

- [Ionic docs](https://ionicframework.com/docs/)
- [A Simple Guide to Navigation in Ionic 2](https://www.joshmorony.com/a-simple-guide-to-navigation-in-ionic-2/)
- [Build a Todo App from Scratch with Ionic](https://www.joshmorony.com/build-a-todo-app-from-scratch-with-ionic-2-video-tutorial/)
- [Deploying to a device and building for production](https://ionicframework.com/docs/intro/deploying/)

### Cordova CLI Reference documentation

- [iOS Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/ios/index.html)
- [Android Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html)

### Troubleshooting

If the `ionic cordova run android` fails because of some license errors, you can accept the licenses by running sdkmanager:

- on Windows: `%ANDROID_HOME%/tools/bin/sdkmanager --licenses` in command prompt
- on Mac/Linux: `$ANDROID_HOME/tools/bin/sdkmanager --licenses` in terminal
