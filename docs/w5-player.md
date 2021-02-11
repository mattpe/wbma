## Week 5/2021

---

## Media Player

### Task A: Modify page for viewing single media files

1. Continue the previous exercise. Create a new git branch 'player' for these tasks.
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

## Task B: Show user's files + update

1. Add new view 'MyFiles.js'
1. Add a button (for example to profile page) which opens MyFiles
1. Display a list of user's own files
    - Very similar to Home
       - You can use List and ListItem as example and make new components.
       - Or you can send props to List and depending the value of the prop show edit and delete buttons (if statement)
       - In both cases make new function useMyMedia() to ApiHooks. It's very similar to 'useLoadMedia'. The difference is that it should return only the logged in users own files.
1. Add 'view', 'modify' and 'delete' buttons next to each file owned by the logged in user
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
    - delete does not need it's own view
       - after deleting use update state in `MainContext` to update the file list.
    - Create _Modify.js_ to _views_ folder. Modify is 90% same as Upload
        - make a copy of Upload.js and remove ImagePicker
        - use PUT instead of POST

### Tips for the project

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
