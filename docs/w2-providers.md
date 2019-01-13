class: center, middle

# WBMA, Ionic Providers, HTTP Client

## 2/2019

---

# Using services

1. Continue last exercise. Create a new branch with git.
1. Create new folder 'services' to 'app'-folder
1. Create new provider 'media' to services folder ```ionic generate provider media```
1. In the provider create a method 'getAllMedia' which fetches all media files from the media API and returns the data
    * example: 
    ```javascript
    ...
    getAllMedia() {    
     return ...http.get(...)
    }
    ...
    ```
    * see Week 1 task 2 for help
1. In HomePage component call 'getAllMedia' and use ```console.log``` to log the returned data 
    - to call getAllMedia, you need to inject MediaProvider to constructor. Call it mediaProvider ```...(private mediaProvider: MediaProvider)```
    
1. Use the existing list in home.html template
    - display image's [thumbnail](http://media.mw.metropolia.fi/wbma/docs/#api-Media-GetFile) version
    - display also image's title and description

---

# HTTP client. Setting headers TODO something else here

1. Create another service to services folder. Call it digitransit It should fetch data from Digitransit Routing API
    - [Documentation](https://digitransit.fi/en/developers/apis/1-routing-api/)
    - [API Documentation](https://api.digitransit.fi/graphiql/hsl), click 'Docs' on the right.
    - base url for Helsinki region: https://api.digitransit.fi/routing/v1/routers/hsl/index/graphql
2. As you read the documentation, you find out that Content-Type must be either “application/graphql” or “application/json”
3. In the digitransit-service create a method that fetches information about routes that go through a certain stop
    - the method should receive the stop name as a parameter
    - it should return Observable
4. Call the method on ListMedia component. Send the name of some nearby bus stop as the parameter (use Google Maps to get stop names) 
5. Create HTML list of bus routes to html-template of ListMedia-component

### Some help

1. [Override request headers](https://angular.io/guide/http#headers)
1. Proxy to bypass CORS:
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
1. Printing data:
    - using expression ```{{ variable }}```
    - iterate repeating data: ```*ngFor```
1. Use [split](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) to change filename extension and add thumbnail size info
    - [Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) to change values all at once`


