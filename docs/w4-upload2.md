class: center, middle

# WBMA, Forms

## 4/2019

---

# Forms, File Upload part 2

## Task 1: Better Upload Page

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Install [Chooser](https://ionicframework.com/docs/v3/native/chooser/) plugin
    - Version 4 should work (`npm install --save @ionic-native/chooser@4` <- _@4_ suffix)
    - [Add to app module](https://ionicframework.com/docs/v3/native/#Add_Plugins_to_Your_App_Module)
1. Use Chooser instead of `<ion-input type="file"...`
    - use e.g. button and click event to start the chooser (_NOTE:_ when inserting more `<button>` elements inside `<form>` element add e.g. `type="button"` attribute to `<button>` to prevent unwanted submission of form)
    - Chooser result is not a File object -> [Blob object](https://developer.mozilla.org/en-US/docs/Web/API/Blob) must be created before appending to [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
    `myBlob = new Blob([chooserResult.data], {type: chooserResult.mediaType});`
    - handle the case where user starts the chooser but cancels before choosing any file
    - set chooser to accept only media files
    - show preview and slider controls only if the file is an image, use some generic placeholder images for audio & video files
1. Upload button should be activated only when the form is correctly filled
    - Title is required and minimun length is ?
    - Description is optional but minimun length is ?
    - Media file of correct type (image/video/audio) is required
1. Add reset button for clearing the whole form and image preview
1. Test in emulator/phone (check: [Debugging in Android devices](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/))

### Troubleshooting

GOT _Failed to load resource: net::ERR_CACHE_MISS_ error on Android? Try:

```sh
ionic cordova platform rm android
ionic cordova platform add android
```

When problems are related to photoviewer plugin, try downgrading to working version or building without it:

1. Remove the plugin: `ionic cordova plugin remove com-sarriaroman-photoviewer`  
1. Try to Install working version of the plugin: `ionic cordova plugin add com-sarriaroman-photoviewer@1.1.18` **or** remove photoviewer all imports & references from `app.module.ts` and your `home` page

Build errors caused by _config.xml_ after adding the chooser plugin? Try **REMOVING** the stuff you might have added there:

```xml
<platform name="android">
 <edit-config
   file="app/src/main/AndroidManifest.xml"
   mode="merge"
   target="/manifest/application">
   <application android:largeHeap="true" />
 </edit-config>
</platform>
```

---

## Task 2 (extra): Use Camera

1. Start camera directly from upload page using [Camera plugin](https://ionicframework.com/docs/v3/native/camera/)
1. Show preview after taking a photo
1. Upload

- Tip: [Converting dataURI to blob](https://stackoverflow.com/questions/4998908/convert-data-uri-to-file-then-append-to-formdata)
- New tip. Old but works: [File Transfer](https://www.djamware.com/post/599da16580aca768e4d2b130/how-to-upload-file-on-ionic-3-using-native-file-transfer-plugin)
