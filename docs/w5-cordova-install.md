# Cordova 
###Install Cordova:
npm install -g cordova

### Make a project folder:
cordova create projectname fi.metropolia.yourname.projectname Projectname

### Go to the project folder:
cd projectname

### Add the platforms you wish to use:
cordova platfortms add ios
cordova platforms add android

### Test app:
cordova run ios/android

## Phone emulators:
1. iOS
  * OS X: Install XCode
  * Windows: http://www.xpadian.com might work

2. Android
  * Windows/OS X/Linux : Install Genymotion and Android Studio

## To test your app:
1. rename app.html to index.html
2. Build your webapp (grunt)
3. modify dist/index.html:
	* add <script src="cordova.js"></script>
4. copy the content of dist-folder to www-folder in the Cordova project
5. Go to the Cordova-project folder and test app: cordova run ios/android

## Example project
[Sound Recorder](https://github.com/ilkkamtk/sound-recorder)
