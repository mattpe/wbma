class: center, middle

# WBMA, Angular Routing & Services

## 3/2017

---
# Routing

#### 1. Create new app with Angular CLI
#### 2. Create components 'front', 'top-bar', 'register' and 'login'
#### 3. Template for 'top-bar' component:
```html
<nav>
  <ul>
    <li>
        <a [routerLink] = "'/front'">Front page</a>
    </li>
    <li>
        <a [routerLink] = "'/login'">Login</a>
    </li>
    <li>
        <a [routerLink] = "'/register'">Register</a>
    </li>
  </ul>
</nav>
```
4. Template for 'front' component:
  ```html
  <div>Display this content when logged in.</div>
  ```
5. Create templates for 'login' and 'register' components yourself
6. For routing edit '/app/app.module.ts/':
- Before @NGModule add this:
  ```typescript
  const routeConfig = [
    {
      path: '',
      pathMatch: 'full',
      redirectTo: '/login'
    },
    {
      path: 'login',
      component: LoginComponent
    },
    {
      path: 'register',
      component: RegisterComponent
    },
    {
      path: 'logout',
      component: LogoutComponent
    },
    {
      path: 'front',
      component: FrontComponent
    }
  ];
  ```
- Edit the imports-array like this:
  ```typescript
  ...
  imports: [
      BrowserModule,
      FormsModule,
      HttpModule,
      RouterModule.forRoot(routeConfig)
    ],
    ...
  ```
7. Edit 'app.component.html' to this:
  ```html
  <app-top-bar></app-top-bar>
  <router-outlet></router-outlet>
  ```
8. Now the navigation should work.

___

# Using services II - Login

1. Create new folder 'services' to 'app'-folder
2. Create new service 'media' to services folder ```ng g s services/media```
3. In the service create methods 'register' and 'login' with corresponding functionalities
- 'login': call media API to login user and save users data to [local storage](http://www.w3schools.com/html/html5_webstorage.asp)
    - when logged in, user is redirected to 'front'
    - if user has already logged in redirect to 'front' (autodirect)
- 'register': call media API to create new user and automatically login


---
# Router basics

Route declarations:

_app.module.ts_
  ```typescript
  ...
  import { RouterModule } from '@angular/router';

  const routeConfig = [
    {
      path: 'example',
      component: ExampleComponent
    }
  ];

  @NgModule({
    ...
    imports: [
      ...
     RouterModule.forRoot(routeConfig),
      ...
    ],
    ...
  ```

`<router-outlet></router-outlet>` declares the placeholder for routed component tree:

_app.component.html_

  ```html
  <h1>App works!</h1>
  <router-outlet></router-outlet>
  ```

---

# Router - Redirects
- By default matching of URLs is done with _startsWith_ algorithm
- `pathMatch: 'full'` can be used to set the algorithm to full matching
- Redirects can be done with `redirectTo`

_app.module.ts_
  ```typescript
  const routeConfig = [
    {
      path: '',
      pathMatch: 'full',
      redirectTo: 'example'
    },
    {
      path: 'example',
      component: ExampleComponent
    }
  ];
  ```
---

# Router - Navigating
- Two ways to navigate between states:
    - Imperatively from within the components code: `this.router.navigateByUrl('example')` or `this.router.navigate(['example'])`
    - Declaratively from within the template: `<div [routerLink]=['example']>`
- URLs starting with `/` are absolute navigations, others relative
- `../` also works for accessing the "parent" URL

_*.component.ts_
  ```typescript
  export class AppComponent {
    constructor(`private router: Router) {
      this.router.navigate(['example']);
    }
  }
  ```

_*.component.html_
  ```html
  <a [routerLink]="['example']">Example</a>
  ```
