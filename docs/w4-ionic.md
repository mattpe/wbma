class: center, middle

# WBMA, Ionic Framework

## Week 4/2018

---

## [Ionic](https://ionicframework.com/docs/)

- uses Angular for application logic
- [UI component library](https://ionicframework.com/docs/components/)
- [icon collection](https://ionicframework.com/docs/ionicons/)
- native capabilities based on [Cordova](https://cordova.apache.org/)
- Note: Old Ionic v1 uses old AngularJS (version 1.x), DO NOT touch that one

### From "native" Angular to Ionic

Main differences in Ionic compared to basic Angular web apps:

- Ionic uses the concept of pages (in Angular everything is just components, in Ionic term "component" refers typically to ready-made [UI components](https://ionicframework.com/docs/components/))
- different routing system, [navigation](https://ionicframework.com/docs//components/#navigation)
  - [NavController & life cycle events](https://ionicframework.com/docs/api/navigation/NavController/)
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
    - choose the default answer (N) for question _'Would you like to integrate your new app with Cordova to target native iOS and Android?'_
    - NOTE: we dont't use ionic1 version or ionic pro services
1. Use Ionic cli to generate pages, `ionic generate page <NAME> [--no-module]`
    - front/home page for media (thumbnail) list view
    - user profile/login/registration pages
    - file upload page
    - use `--no-module` flag if you don't want to create an extra module within your page
1. Generate media provider (service), `ionic generate provider media`
1. Develop & test on browser: `ionic serve` (not 100% reliable, may need restarting after generating new components..)
1. Run & test on mobile device
    - native mobile dev kit is needed, Xcode for iOS or Android SDK for Android
    - add your target platform: `ionic cordova platform add android/ios`
    - connect your device (USB)
    - install & start the app: `ionic cordova run android/ios`

---

### Some docs & tutorials

- [Ionic docs](https://ionicframework.com/docs/): _[Getting started tutorial](https://ionicframework.com/docs/intro/tutorial/)_
- [A Simple Guide to Navigation in Ionic 2](https://www.joshmorony.com/a-simple-guide-to-navigation-in-ionic-2/)
- [Navigation Lifecycle Events](https://blog.ionicframework.com/navigating-lifecycle-events/)
- [Build a Todo App from Scratch with Ionic](https://www.joshmorony.com/build-a-todo-app-from-scratch-with-ionic-2-video-tutorial/)
- [Debugging on a device](https://medium.com/@leetheguy/the-best-way-to-debug-an-ionic-app-on-a-device-79833bef5d1d)
- [Deploying to a device and building for production](https://ionicframework.com/docs/intro/deploying/)

### Some notes

Use media provider only as a data service and build your application logic with pages and components. Api requests done by provider should return observables which are subscribed from page/component. See the example snippets below.

Provider (service):

```js
public getCurrentUser(token: string): Observable<User> {
  const headers = new HttpHeaders().set('x-access-token', token);
  return this.http.get<User>(this.apiUrl + '/users/user', {headers: headers});
}
```

Page (component):

```js
this.myService.getCurrentUser('content.of.tokenstring').subscribe(data => {
  // Do something with the response data
}, (error: HttpErrorResponse) => {
  // Do something with the error object
});
```

`ionic generate` does not modify automatically `app.module.ts` file. Add declarations, entrycomponents and providers manually when needed.

### Cordova CLI Reference documentation

- [iOS Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/ios/index.html)
- [Android Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html)

### Troubleshooting

If the `ionic cordova run android` fails because of some license errors, you can accept the licenses by running sdkmanager:

- on Windows: `%ANDROID_HOME%/tools/bin/sdkmanager --licenses` in command prompt
  - or: `C:\Users\<YOUR_USERNAME>\AppData\Local\Android\sdk\tools\bin\sdkmanager --licenses`
- on Mac/Linux: `$ANDROID_HOME/tools/bin/sdkmanager --licenses` in terminal
