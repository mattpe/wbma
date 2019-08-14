
## 5/2018

---

## Media Player

### Task: Create page for viewing single media files

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Modify 'Single.js'. Features:
    - get a single file from API
    - depending on file type use `<img>`, `<video>` or `<audio>` to show/play media file
        - <http://www.w3schools.com/tags/tag_video.asp>
        - <http://www.w3schools.com/tags/tag_audio.asp>
    - show also other data related to the media file:
        - title
        - description
        - user (to get username you need to request [User endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetUser) using media file's `user_id`)
        - optional: likes (request [Favourite endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-Favourite) on the media api)
            - add likes to image(s) with Postman or add 'like' button to Single.js
        - optional: show users who like the image
 1. - if filters are saved with JSON.strigify in file's description filed like this :
    ```json
      { 
      ...
         "description": "[d]Nice dog[/d][f]{\"brightness\":131,\"contrast\":110,\"warmth\":10,\"saturation\":90}[/f]",
      ...
      }
    ```
    You can extract filters later like this:
    ```javascript
    getFilters = (text) => {
        const pattern = '\\[f\\](.*?)\\[\\/f\\]';
        const re = new RegExp(pattern);
        try {
          return JSON.parse(re.exec(text)[1]);
        } catch (e) {
          // console.log(e);
          return this.state.filters;
        }
      };
    ```
    ...and description like this:
    ```javascript
    getDescription = (text) => {
        const pattern = '\\[d\\]((.|[\\r\\n])*?)\\[\\/d\\]';
        const re = new RegExp(pattern);
        console.log(re.exec(text));
        try {
          return re.exec(text)[1];
        } catch (e) {
          return text;
        }
    };
    ```

## Show user's files + update


1. Add new page 'MyFiles.js'
1. Add a button (for example to profile page) which opens MyFiles
1. Display a list of user's own files
    - very similar to Home
1. Add 'view', 'modify' and 'delete' buttons next to each file.
    - onClick example for delete:
    ```jsx harmony
     <button onClick={() => {
       deleteFile(file_id);
     }}>Delete</button>
    ```
    - important! not like this, because it's invoked immediately without click:
    ```jsx harmony
    <button onClick={ deleteFile(file_id) }>Delete</button>
    ```
1. Add corresponding functionality to the buttons
    - for 'view' use Single.js
    - delete does not need it's own page
    - modify is 90% same as UploadPage
        - make a copy of Upload.js and remove file chooser
        
### Extra. Study how to [protect routes](https://tylermcginnis.com/react-router-protected-routes-authentication/)
### AJAX error handling
```javascript
// MediaAPI.js
const handleFetchErrors = (response) => {
  if (!response.ok) {
    throw Error(response.statusText);
  }
  return response;
}

const getSingleMedia = (id) => {
  return fetch(apiUrl + 'media/' + id)
  .then(handleFetchErrors)
  .then(response => {
    return response.json();
  });
};
```
