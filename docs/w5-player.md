class: center, middle

# WBMA

## 5/2018

---

## Media Player

### Task: Create page for viewing single media files

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Create a new page 'player' (PlayerPage) for viewing single media files. Features:
    - get a single file from API
    - depending on file type use `<img>`, `<video>` or `<audio>` to show/play media file
        - <http://www.w3schools.com/tags/tag_video.asp>
        - <http://www.w3schools.com/tags/tag_audio.asp>
    - show also other data related to the media file:
        - title
        - description
        - user (to get username you need to request [User endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetUser) using media file's `user_id`)
        - optional: likes (request [Favourite endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-Favourite) on the media api)
            - add likes to image(s) with Postman or add 'like' button to PlayerPage
        - optional: show users who like the image
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
 1. To use CSS filters get rid of Photo Viewer plugin and use `img` element instead
    - you can use [Pinch zoom npm plugin](http://crystalui.org/components/pinch-zoom) to add similar behavios as Photo Viewer plugin
    - if filters are saved with JSON.strigify in file's description filed like this :
    ```json
      { 
      ...
         "description": "[d]Nice dog[/d][f]{\"brightness\":131,\"contrast\":110,\"warmth\":10,\"saturation\":90}[/f]",
      ...
      }
    ```
    You can extract filters later like this:
    ```javascript
    const pattern = '\\[f\\](.*?)\\[\\/f\\]';
        const re = new RegExp(pattern);
        // console.log(re.exec(value));
        try {
          return JSON.parse(re.exec(value)[1]);
        } catch (e) {
          return {
            brightness: 100,
            contrast: 100,
            warmth: 0,
            saturation: 100,
          };
        }
       ```

## Show user's files + update


1. Add new page 'my-files' (MyFilesPage)
1. Add a button (for example to profile page) which opens MyFilesPage
1. Display a list of user's own files
    - very similar to HomePage
1. Add 'view', 'modify' and 'delete' buttons next to each file.
1. Add corresponding functionality to the buttons
    - for 'view' use PlayerPage
    - delete does not need it's own page
    - modify is 90% same as UploadPage
        - make a copy of upload.html and remove file chooser
