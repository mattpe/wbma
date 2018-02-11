class: center, middle

# WBMA

## 4/2017

---

# Media Player

### Task: Create component for viewing single media files

1. Use the previous [exercise](w3-upload.md) as a starting point and develop it further
1. Create a new component for viewing single media files. Features:
    - get a single file from API
    - depending on file type use `<img>`, `<video>` or `<audio>` to show/play media file
        - <http://www.w3schools.com/tags/tag_video.asp>
        - <http://www.w3schools.com/tags/tag_audio.asp>  
    - show also other data related to the media file:
        - title
        - description
        - user (to get username you need to request [User endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetUser) using media file's `user_id`)
        - likes (request [Favourite endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-Favourite) on the media api)
        - liked by user
1. Some help:
    - Sending parameters
    
        ```TypeScript
        someFunction(param1, param2) {
            this.navCtrl.push(SomePage, {
              property1: param1,
              property2: param2
            });
          }
        ```
    - To use parameters: https://ionicframework.com/docs/api/navigation/NavParams/
    
## Extra 

### Extract EXIF-data from image
1. Install [exif.js](https://github.com/exif-js/exif-js) with npm
1. Import to component/page: 

    ```TypeScript
        ...
        import {EXIF} from 'exif-js';
        ...
        getExif(evt) {
            try {
              EXIF.getData(evt.target, () => {
                // console.log(EXIF.getAllTags(evt.target));
                if (EXIF.getTag(evt.target, 'GPSLatitude')) {
                  this.lat = this.degreesToDecimals(
                      EXIF.getTag(evt.target, 'GPSLatitude'));
                  this.lon = this.degreesToDecimals(
                      EXIF.getTag(evt.target, 'GPSLongitude'));
                } else {
                  this.message = 'No GPS data';
                }
              });
            } catch (e) {
              console.log(e);
            }
        }
    ```
1. Call getExif() on <img> element's load event.
1. To use GPS coordinates with Google Maps, you need to convert them to decimals:
    ```TypeScript
        degreesToDecimals(deg: Array<number>): number {
            return deg[0]['numerator'] + (deg[1]['numerator'] / 60) +
                (deg[2]['numerator'] / 100 / 3600);
          }
    ```
