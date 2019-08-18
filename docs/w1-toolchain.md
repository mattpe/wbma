class: center, middle

# Toolchain

## 1/2019

---

# Contents

- Editor/IDE: WebStrom/PhpStorm, Visual Studio Code, (or any)
- Language: JavaScript (ES6 ->)
- Run, test & debug: Chrome browser dev tools, Safari browser dev tools
- Version Control System: Git
- Package manager: NPM or Yarn
- Building & automating tasks: Expo
- Development frameworks: React Native

---

# Code editor or IDE

Ultimately, it's your choice. VSCode is recommended.

#### Visual Studio Code

- free & open source code editor by Microsoft (**!=** Visual Studio IDE)
- wide extension support
- lightweight, multiplatform support
- good [docs & instructions](https://code.visualstudio.com/docs/editor/codebasics)
- choice of many React developers

# Install Extensions

Press _ctrl-shift-x_ or click extensions icon on the left panel.

Search and install:

- EditorConfig for VS Code
- Auto Import
- ESLint
- JavaScript (ES6) Code Snippets
- React Pure To Class
- React-Native/React/Redux snippets for es6/es7


Other handy extensions:

- Duplicate file: Add _right-click -> Duplicate file_ action
- Prettier: Code formatter
    
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

(Windows users only) Change integrated console to Bash in Windows:

1. Install [Git for Windows](https://git-scm.com/downloads) to default location
2. Edit vscode settings file (_File -> Preferences -> Settings_) and search for 'terminal'. 
- Change 'Terminal › External: Windows Exec' value to "C:\\Program Files\\Git\\bin\\bash.exe"

---

#### WebStorm/PhpStorm

- free for Metropolia students. [Apply for license here](https://www.jetbrains.com/student/)
  - _@metropolia.fi_ email address needed for a free license
- full featured IDE
- quite ready out of the box. No need for plugins.
- based on IntelliJ IDEA, just like Android Studio

#### Other picks

- [Atom](https://atom.io/)
- [Brackets](http://brackets.io/)
- Other IDEs like: IntelliJ Ultimate IDEA, Eclipse, NetBeans... 

---

# Browser & debugging

- Chrome & [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
- Safari & [Safari Develop menu](https://support.apple.com/guide/safari/use-the-developer-tools-in-the-develop-menu-sfri20948/mac)

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

- IDE specific project files & folders (.idea)
- build targets and other automatically generated files
- packages managed e.g. by npm or bower (= _node_modules/_ & _bower_components/_ folders) 
- any temp & OS specific files, like Apple's `.DS_Store` 

Expo generates a .gitignore file automatically.

---

# Package Management

## [NPM](https://www.npmjs.com/) - Node.js Package Manager

- Install [node.js](https://nodejs.org/en/) to get the package manager **npm**
- npm packages needed in a project (dependencies) are listed in the `package.json` file and can be install with `npm install` command
- locally installed (=project specific) packages are downloaded to `node_modules/` folder (should be excluded from version control)

#### OS X no sudo for Mac users

- [instructions](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md)

#### NPM Alternative

[Yarn](https://yarnpkg.com/) 

- newcomer gaining a lot of traction now
- first [open source release on October, 2016](https://code.facebook.com/posts/1840075619545360). Current version 0.18.1 
- uses same package.json file and npm registry as npm
- claimed to be faster, more secure and reliable but npm has been catching up

---

# Example package.json

```javascript
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

