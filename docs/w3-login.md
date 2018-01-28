class: center, middle

# WBMA, Angular Routing & Services

## 3/2018

---
# Routing

1. Create new app with Angular CLI. Add routing and style=scss [options](https://github.com/angular/angular-cli/wiki/new)
2. Create components 'front', 'top-bar', 'register', 'login' and 'logout'
3. Template for 'top-bar' component:

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
6. For routing edit '/app/app-routing.module.ts/':
- Add this:

  ```typescript
  const routes: Routes = [
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

7. Edit 'app.component.html' to this:

  ```html
  <app-top-bar></app-top-bar>
  <router-outlet></router-outlet>
  ```
8. Now the navigation should work.

___

# Using services II - Login

1. Create new service 'media' to services folder ```ng g s services/media```
2. In the service create methods 'register' and 'login' with corresponding functionalities
 'login': call media API to login user and save users token to [local storage](http://www.w3schools.com/html/html5_webstorage.asp)
    - when logged in, user is redirected to 'front'
    - if user has already logged in redirect to 'front' (autodirect)
- 'register': call media API to create new user and automatically login


---
# Router basics

- [angular.io guide](https://angular.io/guide/router)
- [Angular CLI routing](https://coursetro.com/posts/code/111/Using-the-Angular-5-Router-%28Tutorial)

- When using Angular CLI use --routing option

Route declarations:

_app-routing.module.ts_
```typescript
...
import { ExampleComponent } from './example/example.component';

const routes: Routes = [
  {
    path: 'example',
    component: ExampleComponent
  }
];
  ...
```

- `<router-outlet></router-outlet>` declares the placeholder for routed component tree:

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

_app-routing.module.ts_
```typescript
const routes: Routes = [
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
  constructor(private router: Router) {
  this.router.navigate(['example']);
  }
}
```

_*.component.html_
```html
<a [routerLink]="['example']">Example</a>
```

