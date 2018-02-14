class: center, middle

# Image Editor

## 5/2018

### Make sure your Android Studio, SDK and Emulator are up to date

---
1. Load this repo as zip: https://github.com/ilkkamtk/mediaApp2 and extract
2. Run `npm install` to load neccessary packages
3. To make cordova.js available in Android emulator edit `node_modules/@ionic/app-scripts/dist/dev-server/serve-config.js`:
    * replace last row with this: 
    ```
    exports.ANDROID_PLATFORM_PATH = path.join('platforms', 'android', 'app/src/main', 'assets', 'www');
    ```
4. Try to build: `ionic cordova build android` or `ionic cordova build ios`
    * Fix possible linting errors (red color) and try to build again
5. On android Google Maps and geolocation plugins are clashing. Fix it by editing `plugins/cordova-plugin-geolocation/plugin.xml`:
    * remove `<uses-feature android:name="android.hardware.location.gps" />`
    * remove and re-add Android platform
        ```
        ionic cordova platform rm android
        ionic cordova platform add android
        ```
6. Run app on emulator or device to make sure everything is working.
7. Use the BrightContrast method in EditorProvider as an example to create a color filter and autocontrast. Use the formulas below.

## Extra 

Add grayscale conversion (checkbox). The human eye sees green a bit better than red and blue, so use luma coefficients to compensate that:
- R: 0.2126
- G: 0.7152
- B: 0.0722
___

### Formulas:
#### Brightness/contrast:

`Po = (P - 128) * C + 128 + B`

P = Pixel value

C = Contrast (range input 0-10, step 0.1)

B = brightness (range input -255 - 255, step 1)

#### Color filter: 

`Po = P + R / (101 - S)`

P = Pixel value

R = color value R/G/B (3 range inputs 0-255, step 1)

S = Strength (range input 0-100, step 1)



#### Autocontrast (checkbox):

`Po = (P - mi)/(ma - mi) * 255`

P = Pixel value

mi = minimum pixel value

ma = maximum pixel value

### Links:
- [Canvas](http://www.w3schools.com/html/html5_canvas.asp)
- [FileReader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader)
- [Image Editing Tutorial](https://www.html5rocks.com/en/tutorials/canvas/imagefilters/)
- [WebGL library for image editing](http://evanw.github.io/glfx.js/)
