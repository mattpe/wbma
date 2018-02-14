class: center, middle

# WBMA, Angular HTTP Client

## 2/2018

---

# Using services

1. Create new app with Angular CLI
2. Create new folder 'services' to 'app'-folder
3. Create new service 'media' to services folder ```ng g s services/media```
4. In the service create a method 'getAllMedia' which fetches all media files from the media API and returns the data as Observable
    * example: 
    ```javascript
    ...
    getAllMedia() {    
     return ...http.get(...)
    }
    ...
    ```
    * see Week 1 task 2 for help
5. Create new component 'listMedia' 
6. Call 'getAllMedia' on ListMedia component and use ```console.log``` to log the returned data 
    - to call getAllMedia, you need to inject MediaService to constructor. Call it mediaService ```...(private mediaService: MediaService)```
    
7. Create HTML list of images to template of ListMedia-component
    - display image's [thumbnail](http://media.mw.metropolia.fi/wbma/docs/#api-Media-GetFile) version
    - display also image's title and description

---

# HTTP client. Setting headers

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
2. [Bypass CORS if needed](https://www.thepolyglotdeveloper.com/2014/08/bypass-cors-errors-testing-apis-locally/)
3. Printing data:
    - using expression ```{{ variable }}```
    - iterate repeating data: ```*ngFor```
4. Use [split](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) to change filename extension and add thumbnail size info
    - [Array.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) to change values all at once


### Extra. Add Bootstrap
1. Add the Bootstrap 4 library to your project: ```npm install --save bootstrap@next```
2. Add the following line in file styles.css: ```@import "~bootstrap/dist/css/bootstrap.css";```
3. Bootstrap JavaScript library is making use of jQuery and is manipulating the DOM directly. For an Angular application any direct DOM manipulations should be avoided and the complete control to update DOM elements should be be given to the Angular framework. Use Bootstrap 4 Angular directives: ```npm install --save @ng-bootstrap/ng-bootstrap```
4. Having completed the installation the corresponding Angular module NgbModule must be imported in app.module.ts:
   ```
   import { NgbModule } from '@ng-bootstrap/ng-bootstrap';
   ```
5. NgbModule needs to be added to the imports array by calling the forRoot() method as you can see in the following:
   ```
   imports: [
       ...,
       NgbModule.forRoot()
     ],
   ```


