class: center, middle

# WBMA, Ionic HTTP Client

## 1/2019

---

# Fetching data with HTTP Client, Task A

1. Continue last exercise. Create a new branch with git.
1. Save [test.json](./assets/test.json) into 'assets' folder of your project.
1. Create new interface 'Pic'
    - add folder 'interfaces' to 'src', create new file there 'pic.ts'
    - move Pic-class to pic.ts and convert it to [array type interface](http://techfunda.com/howto/1079/array-and-class-types-interfaces)
1. Import HttpClientModule in app.module.ts
1. In HomePage component, inject HttpClient to constructor and create a method which fetches 'test.json' file either with GET or POST
    - Example 
    ```typescript
    ...
    constructor(... public http: HttpClient ...) {
    
    }
    ...
     this.http.get('example.json').subscribe((res:Response) => this.someVariable = res.json());
    ...
    ```
1. First log the data using ```console.log()```
1. Then print the data to the list in home.html

---

# Fetching data with HTTP Client, Task B

1. Continue last exercise. Create a new branch with git.
1. Modify the app so that you fetch the data from the media API instead of test.json
    - [Documentation](http://media.mw.metropolia.fi/wbma/docs/)
    - base url: http://media.mw.metropolia.fi/wbma/
    - Media files location: http://media.mw.metropolia.fi/wbma/uploads/
1. First log the data using ```console.log()```
1. Then print the data to the list in home.html

### Some help

1. Remember to import the Http class to the component and also inject the Http class to constructor
2. [Http class](https://angular.io/docs/ts/latest/api/http/index/Http-class.html)
3. [Bypass CORS if needed](https://www.thepolyglotdeveloper.com/2014/08/bypass-cors-errors-testing-apis-locally/)
4. Printing data:
    - using expression ```{{ variable }}```
    - [iterate repeating data](https://angular.io/api/common/NgForOf): ```*ngFor```
