
## 5/2018

---

## Media Player

### Task: Create page for viewing single media files

1. Continue the previous exercise. Create a new git branch for these tasks.
1. Modify 'Single.js'. Features:
    - depending on file type use `<Image>` or `<Video>` to show/play media file
        - https://docs.expo.io/versions/latest/sdk/video/
        - Audio is optional: https://docs.expo.io/versions/latest/sdk/audio/
    - show also other data related to the media file:
        - title
        - description
        - user (to get username you need to request [User endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetUser) using media file's `user_id`)
        - optional: likes (request [Favourite endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-Favourite) on the media api)
            - add likes to image(s) with Postman or add 'like' button to Single.js
        - optional: show users who like the image

## Show user's files + update

1. Add new view 'MyFiles.js'
1. Add a button (for example to profile page) which opens MyFiles
1. Display a list of user's own files
    - very similar to Home (and List)
1. Add 'view', 'modify' and 'delete' buttons next to each file.
    - onPress example for delete:
    ```jsx harmony
     <Button onPress={() => {
       deleteFile(file.file_id);
     }}><Text>Delete</Text></Button>
    ```
    - important! not like this, because it's invoked immediately without click:
    ```jsx harmony
    <Button onPress={ deleteFile(file.file_id) }>...
    ```
1. Add corresponding functionality to the buttons
    - for 'view' use Single.js
    - delete does not need it's own page
    - modify is 90% same as Upload
        - make a copy of Upload.js and remove ImagePicker

### Tips for project
- Add a tag with your app name automatically to all uploaded files. This way they don't get mixed with files uploaded by other apps.
- If you want to save additional data with files, you can add it to the 'description' like this:
    ```javascript
      
      ...
      const moreData = {
        description: 'This is the actual description',
        someData: 'Some other data I want to save',
        someMoreData: {width: 300, height: 450 } 
      }
      ...
          // FormData
         formData.append('description', JSON.stringify(moreData));
      ...
      
    ```
    You can extract data later like this:
    ```javascript
    const allData = JSON.parse(descriptionFromAPI);
    const description = allData.description;
    const someData = allData.someData;
    const someMoreData = allData.someMoreData;
    ```