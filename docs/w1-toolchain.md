class: center, middle

# Mobile Web Development Toolchain


## 1/2017

---

# Contents

- Editor/IDE: Visual Studio Code, vscode (or any)
- Language: TypeScript
- Run, test & debug: Chrome browser dev tools       
- Version Control System: Git
- Package manager: NPM
- Building & automating tasks: Angular CLI (webpack)
- Development frameworks: Angular 2, Ionic 2
- Creating a native (hybrid) app: Ionic 2 (Cordova)

---

# Code editor or IDE

Ultimately, it's your choice. VSCode is recommended.

#### Visual Studio Code

- free & open source code editor by Microsoft (**!=** Visual Studio IDE)
- wide extension support
- lightweight, multiplatform support
- good [docs & instructions](https://code.visualstudio.com/docs/editor/codebasics)
- choice of many Angular2 developers

#### Other picks

- [Atom](https://atom.io/)
- [Brackets](http://brackets.io/)
- [WebStorm](https://www.jetbrains.com/webstorm/)
  - free student license (only @metropolia.fi email address needed)
  - full featured IDE
  - based on IntelliJ IDEA, just like Android Studio
- Other IDEs like: IntelliJ Ultimate IDEA, Eclipse, NetBeans... 

---

# Browser & debugging

- Chrome & [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
- [Augury](https://augury.angular.io/) browser extension for Angular 2 debugging

![Chrome screenshot](images/chrome-devtools.png)

---

# Source Code Management - Git

Check [Git stuff](https://github.com/mattpe/git-intro/blob/master/git-basics.md)

What files to include in repo?

- all source code
- README.md and other documentation
- eg. npm grunt or bower settings files
- .gitignore file: list of local stuff not to be included in the version control ->

Exclude:

- IDE specific project files & folders
- build targets and other automatically generated files
- packages managed e.g. by npm or bower (= _node_modules/_ & _bower_components/_ folders) 
- any temp & OS specific files, like Apple's `.DS_Store` 

---

# Package Management

## [NPM](https://www.npmjs.com/) - Node.js Package Manager

- Install [node.js](https://nodejs.org/en/) to get the package manager **npm**
- npm packages needed in a project (dependencies) are listed in the `package.json` file and can be install with `npm install` command
- locally installed (=project specific) packages are downloaded to `node_modules/` folder (should be excluded from version control)

#### Alternative

[Yarn](https://yarnpkg.com/) 

- newcomer gaining a lot of traction now
- first [open source release on October, 2016](https://code.facebook.com/posts/1840075619545360). Current version 0.18.1 
- uses same package.json file and npm registry as npm
- claimed to be faster, more secure and reliable 

---

# Example package.json

```js
{
  "name": "example-app",
  "version": "0.0.1",
  "author": "Example Coder <ecoder@example.com>",
  "description": "An example app doing something",
  "license": "MIT",
  "scripts": {
    "start": "node ./app.js"
  },
  "dependencies": {
    "@angular/common": "~2.1.0",
    "@angular/core": "~2.1.0"
  }        }
}

```

---

# Automating Development Tasks

**[angular-cli](https://github.com/angular/angular-cli#angular-cli) command line tool** - `ng` command:

- Run frequent routine tasks in development workflow easily
- Create an app skeleton
- Generate app components 
- Run development server enviroment
- Run tests, validate code
- Build/Deploy application
  - Minify & combine source files
  - Remove comments & other extra stuff not needed in production version
- project specific settings in _angular-cli.json_ file

#### Other generic JS task runners

- [Grunt](http://gruntjs.com/) & Gruntfile.js (like make & makefile in C)
- [Gulp](http://gulpjs.com/) & Gulpfile.js 

---

# Frameworks used

## Front-end application logic

[Angular 2](https://angular.io/)

## Layout HTML/CSS components & Hybrid app

[Ionic 2](https://ionicframework.com/) 

---

# From web page to native app

## Hybrid App

- Written in HTML/CSS/JS
- Wrapped to native app using packaging tool
- [Apache Cordova](https://cordova.apache.org/)
  - Create mobile apps with HTML, CSS & JS
- [Ionic Framework](http://ionicframework.com)
  - uses Cordova for building
  - utilizes Angular for application logic
  - has it's own HTML/CSS components

---

class: center, middle

# Getting Started with VSCode

---
        
# Install the Editor

Download & install [Visual Studio Code](https://code.visualstudio.com/)
        
.center[![VSCode logo](images/vscode.png)]

---

# Install Extensions

Press _ctrl-shift-x_ or click extensions icon on the left panel.

Search and install:

- Auto Import
- TSLint

Other handy extensions:

- EditorConfig for VS Code: support for [EditorConfig](http://editorconfig.org/)
- Duplicate file: Add _right-click -> Duplicate file_ action
    
---

# VSCode - Basic Usage

Active **project** is the folder open on the left side panel (_File -> Open folder..._) 

Handy keyboard shortcuts (finnish layout, check _File -> Preferences -> Keyboard shortcuts_ for more)        

- Multiline comment: _ctrl-'_
- Delete line: _ctrl-shift-k_
- Move line(s): _alt-up/down_
- Copy line(s): _alt-shift-up/down_
- Auto format code: _alt-shift-f_
- Open integrated console: _ctrl-ö_
- Quick find/open files: _ctrl-p_
- Split editor: _ctrl-§_

---

# VSCode - Settings

Change integrated console to Bash in Windows:

1. Install [Git for Windows](https://git-scm.com/downloads) to default location
2. Edit vscode settings file (_File -> Preferences -> User settings_) and add the following property into json object:

```js
// Place your settings in this file to overwrite the default settings
{
  "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
}
```

---

# Exercise 1: Setup your toolchain and a new Angular 2 project

**a.**

1. Install code editor + extensions, git, npm and angular-cli
2. Use angular-cli to generate the app skeleton ([set style type to _scss_](https://github.com/angular/angular-cli#global-styles)).
3. Test that app works, run with angular-cli and open in browser
4. Create a remote git repository (github/bitbucket) and push your app there
5. If not public, share your repo to both teacher accounts: _mattpe_ & _ilkkamtk_ and return the repo link to tuubi.

**b.**

1. develop your app further following the [Note card tutorial](http://courses.angularclass.com/courses/angular-2-fundamentals/lectures/1280055) but use now `ng` command to generate components.
2. git add, commit & push to remote repository 
3. goto b 1.

---

## Useful online material

Check [Readme file](https://github.com/mattpe/wbma) of this repo.
