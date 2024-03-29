# Web Based Mobile Applications

## Toolchain

---

## Contents

- Editor/IDE: Visual Studio Code (or WebStrom/PhpStorm or any)
- Language: JavaScript (ES6 ->)
- Run, test & debug: browser + dev tools, expo + device/emulator
- Version Control System: Git
- Package manager: NPM (or Yarn)
- Building & automating tasks: Expo
- Development frameworks: React Native

---

## Code editor or IDE

Ultimately, it's your choice. VSCode is recommended.

### Visual Studio Code

- free & open source code editor by Microsoft (**!=** Visual Studio IDE)
- wide extension support
- lightweight, multiplatform support
- good [docs & instructions](https://code.visualstudio.com/docs/editor/codebasics)
- choice of many React developers

#### Install Extensions

Press _ctrl-shift-x_ or click extensions icon on the left panel.

Search and install:

- Prettier
- EditorConfig for VS Code
- Auto Import
- ESLint
- JavaScript (ES6) Code Snippets
- ES7 React/Redux/GraphQL/React-Native snippets

#### VSCode - Basic Usage

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

#### VSCode - Settings

(Windows users only) Change integrated console to Bash in Windows:

1. Install [Git for Windows](https://git-scm.com/downloads) to default location
2. Edit vscode settings file (_File -> Preferences -> Settings_) and search for 'terminal'.
3. Change 'Terminal › External: Windows Exec' value to "C:\\Program Files\\Git\\bin\\bash.exe"

---

### WebStorm/PhpStorm

- free for Metropolia students. [Apply for license here](https://www.jetbrains.com/student/)
  - _@metropolia.fi_ email address needed for a free license
- full featured IDE
- quite ready out of the box. No need for plugins.
- based on IntelliJ IDEA, just like Android Studio

- Other IDEs like: IntelliJ Ultimate IDEA, Eclipse, NetBeans, etc. could work too

---

## Browser & debugging

- Chrome & [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
- Safari & [Safari Develop menu](https://support.apple.com/guide/safari/use-the-developer-tools-in-the-develop-menu-sfri20948/mac)

![Chrome screenshot](images/chrome-devtools.png)

- [Expo Client](#expo)

---

## Source Code Management - Git

Check [Git stuff](https://github.com/mattpe/git-intro/blob/master/git-basics.md)

What files to include in repo?

- all source code
- README.md and other documentation
- npm, .editorconfig, linter, etc. project specific config files
- .gitignore file: list of local stuff not to be included in the version control

Exclude:

- IDE specific project files & folders (.idea)
- build targets and other automatically generated files
- packages managed e.g. by npm or bower (= _node_modules/_ & _bower_components/_ folders)
- any temp & OS specific files, like Apple's `.DS_Store`

[Expo cli](#expo) generates a .gitignore file automatically.

---

## Package Management

### [NPM](https://www.npmjs.com/) - Node.js Package Manager

- Install [node.js](https://nodejs.org/en/) to get the package manager **npm**
- npm packages needed in a project (dependencies) are listed in the `package.json` file and can be install with `npm install` command
- locally installed (=project specific) packages are downloaded to `node_modules/` folder (should be excluded from version control)

### OS X no sudo for Mac users

MacOS no sudo for Mac users!!
* Older MacOS (bash terminal)
```
mkdir ~/.npm-packages
npm config set prefix ~/.npm-packages
echo NPM_PACKAGES="${HOME}/.npm-packages" >> ${HOME}/.bashrc
echo prefix=${HOME}/.npm-packages >> ${HOME}/.npmrc
echo NODE_PATH=\"\$NPM_PACKAGES/lib/node_modules:\$NODE_PATH\" >> ${HOME}/.bashrc
echo PATH=\"\$NPM_PACKAGES/bin:\$PATH\" >> ${HOME}/.bashrc
echo source "~/.bashrc" >> ${HOME}/.bash_profile
source ~/.bashrc
```
* Newer MacOS (zsh terminal)
```
mkdir ~/.npm-packages
npm config set prefix ~/.npm-packages
echo NPM_PACKAGES="${HOME}/.npm-packages" >> ${HOME}/.zshrc
echo prefix=${HOME}/.npm-packages >> ${HOME}/.npmrc
echo NODE_PATH=\"\$NPM_PACKAGES/lib/node_modules:\$NODE_PATH\" >> ${HOME}/.zshrc
echo PATH=\"\$NPM_PACKAGES/bin:\$PATH\" >> ${HOME}/.zshrc
echo source "~/.zshrc" >> ${HOME}/.zsh_profile
source ~/.zshrc
```

### NPM Alternative

[Yarn](https://yarnpkg.com/)

- newcomer gaining a lot of traction
- first [open source release on October, 2016](https://code.facebook.com/posts/1840075619545360)
- uses same package.json file and npm registry as npm
- claimed to be faster, more secure and reliable but npm has been catching up

---

## React Native Development Tools

### Expo

<https://expo.io/learn>

- _Expo CLI_ command line tool: bootstrap, serve, share, build, and publish apps
- _Expo Client_ [Android/iOS](https://expo.io/tools#client) app: test & run apps on device before deploying
- _Expo SDK_ libraries: access native device APIs
- (_[Snack](https://snack.expo.io/)_: Online development enviroment)

Original CRNA (`create-react-native-app`) bootstrapping has been deprecated since the CRNA project was merged with Expo

### Example package.json

Generated by Expo cli.

```javascript
{
  "main": "node_modules/expo/AppEntry.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web",
    "eject": "expo eject"
  },
  "dependencies": {
    "expo": "~36.0.0",
    "react": "~16.9.0",
    "react-dom": "~16.9.0",
    "react-native": "https://github.com/expo/react-native/archive/sdk-36.0.0.tar.gz",
    "react-native-web": "~0.11.7"
  },
  "devDependencies": {
    "babel-preset-expo": "~8.0.0",
    "@babel/core": "^7.0.0"
  },
  "private": true
}

```
