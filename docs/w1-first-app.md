# Exercise 1: Setup your toolchain and a new Ionic project

**a.**

Check: [Ionic docs](https://ionicframework.com/getting-started#cli)

1. If needed, install code editor (+ extensions), git, npm
1. Install Ionic `npm install -g ionic`
1. If you want to use iOS install ios-deploy `npm install -g ios-deploy`
1. Use the `ionic` cli tool to generate a _blank_ app skeleton `ionic start myFirstApp blank`
   1. Answer no to 4.0 and appflow suggestions 
1. Test that app works, run it with `ionic <command>` and open in browser
   - `cd myFirstApp`
   - `ionic serve`
1. Create a remote git repository and push your app there

**b.**  
1. Install TSlint to your project `npm i -D tslint tslint-ionic-rules` 
1. [Enable TSLint in your project](https://www.jetbrains.com/help/webstorm/tslint.html)
   - tslint.json contents:
   ```json
   {
     "defaultSeverity": "warning",
     "extends": "tslint-ionic-rules",
     "jsRules": {},
     "rules": {
       "no-duplicate-variable": true,
       "no-floating-promises": {
         "severity": "error"
       },
       "promise-function-async": true,
       "no-unused-variable": [
         true
       ],
       "no-var-requires": false
     },
     "rulesDirectory": [
       "node_modules/tslint-eslint-rules/dist/rules"
     ]
   }
   ```
1. Run `npm run lint` and fix possible errors in your code.
1. You can edit settings/editor/code style/typescript to correct code automatically with ctr-alt-l

**c.**



1. develop your app further. Add parts to the app skeleton so that the layout is similar to [this](https://cdn.tutsplus.com/net/uploads/legacy/397_yourFirstdesign/images/2.jpg)
1. git add, commit & push to remote repository 
1. goto b 1 and add content (text, images) and more CSS.

---