class: center, middle

# WBMA, Ionic Providers, HTTP Client

## 2/2019

---

# Using providers A

1. Continue last exercise. Create a new branch with git.
1. Create new provider 'media' ```ionic generate provider media```
1. In the provider create a method 'getAllMedia' which fetches all media files from the media API and returns the data as Observable
    * example: 
    ```javascript
    ...
    getAllMedia() {    
     return ...httpClient.get<type>(...)
    }
    ...
    ```
    * see Week 1 task 2 for help
1. Add the provider to 'app.module.ts'
1. In HomePage component create a function 'getAllFiles' which is called on 'ionViewDidLoad'. In 'getAllFiles' call getAllMedia' and use ```console.log``` to log the returned data 
    - To call getAllMedia, you need to inject MediaProvider to constructor. Call it mediaProvider ```...(private mediaProvider: MediaProvider)```
    
1. Use the existing list in home.html template
    - Display image's [thumbnail](http://media.mw.metropolia.fi/wbma/docs/#api-Media-GetFile) version
    - Use [String.split](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) to change filename extension and add thumbnail size info
        - [Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) to change values all at once` 
    - Display also image's title and description

---

# Using providers B

1. In MediaProvider create method 'getSingleMedia(id)' which fetches single media file defined by id parameter.
1. In HomePage component modify 'getAllFiles' so that you get files with thumbnails by using 'getSingleMedia(id)' instead of String.split
    


### Some help

1. Proxy to bypass CORS if neccessary:
    ```json
    // add to ionic.config.json
    {
    ...
         "proxies": [
           {
             "path":"/api",
             "proxyUrl": "http://media.mw.metropolia.fi/wbma"
           }
         ],
      ...
    }
    ```
