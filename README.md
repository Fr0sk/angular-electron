[![Angular Logo](./logo-angular.jpg)](https://angular.io/) [![Electron Logo](./logo-electron.jpg)](https://electron.atom.io/)


[![Travis Build Status][build-badge]][build]
[![Dependencies Status][dependencyci-badge]][dependencyci]
[![Make a pull request][prs-badge]][prs]
[![Apache 2 License][license-badge]][license]
[![Donate][donate-badge]][donate]

[![Watch on GitHub][github-watch-badge]][github-watch]
[![Star on GitHub][github-star-badge]][github-star]
[![Tweet][twitter-badge]][twitter]

# Introduction

Bootstrap and package your project with Angular 4(+) and Electron (Typescript + SASS + Hot Reload) for creating Desktop applications.
Includes Angular Material and Material Icon font.

Currently runs with:

- Angular v5.2.0
- Angular-CLI v1.6.4
- Angular Material 5.0.4
- Electron v1.7.10
- Electron Builder v19.52.1

With this sample, you can :

- Run your app in a local development environment with Electron & Hot reload
- Run your app in a production environment
- Package your app into an executable file for Linux, Windows & Mac

## Getting Started

Clone this repository locally :

``` bash
git clone https://github.com/maximegris/angular-electron.git
```

Install dependencies with npm :

``` bash
npm install
```

There is an issue with `yarn` and `node_modules` that are only used in electron on the backend when the application is built by the packager. Please use `npm` as dependencies manager.

If you want to generate Angular components with Angular-cli , you **MUST** install `@angular/cli` in npm global context.  
Please follow [Angular-cli documentation](https://github.com/angular/angular-cli) if you had installed a previous version of `angular-cli`.

``` bash
npm install -g @angular/cli
```

## Notes (changes from original project)

This project adds [Angular Material](https://material.angular.io/) and [Material Icons](https://material.io/icons/) to ease up making the User Interface. It also has nodemon to restart the app when the Electorn code is changed.

The directory structure was tweaked up a bit. Electron code is in the `/src` folder and Angular code is in the `/view` folder.

To reference the root of the project in Electron you should use `app.getAppPath()`, since `__dirname` will point to `/src`, although for most cases using `__dirname` will not bring any problems.

When using portable builds (at least on Windows), the `app.getAppPath()` and `__dirname` will point to inside the `.asar` in a temporary folder. To get the path where the application was launched (say, to save files within the executable) the environment variable `PORTABLE_EXECUTABLE_DIR` is set on launching. Access it inside the application code using `process.env.PORTABLE_EXECUTABLE_DIR`.
This last bit is not a change to the original project but rather a tip that took me a while to find (I must say, I was not used to Electron Builder).


## To build for development

- **in a terminal window** -> npm start  
- **in another terminal window** -> npm run electron:serve

Voila! You can use your Angular + Angular Material + Electron app in a local development environment with hot reload and auto-restart!

The application code is managed by `src/main.ts`. In this sample, the app runs with a simple Electron window and "Developer Tools" is open.  
The Angular code is in the `view/` directory. The component contains an example of Electron and NodeJS native lib import. See [Use NodeJS Native libraries](#use-nodejs-native-libraries) charpter if you want to import other native libraries in your project.  
You can desactivate "Developer Tools" by commenting `win.webContents.openDevTools();` in `src/main.ts`.

## To build for production

- Using development variables (environments/index.ts) :  `npm run electron:dev`
- Using production variables (environments/index.prod.ts) :  `npm run electron:prod`

Your built files are in the /dist folder.

## Included Commands

|Command|Description|
|--|--|
|`npm run start:web`| Execute the app in the brower |
|`npm run build:linux`| Builds your application and creates an app consumable on linux system |
|`npm run build:mac`|  On a MAC OS, builds your application and generates a `.app` file of your application that can be run on Ma |
|`npm run build:win`| On a Windows OS, builds your application and creates an app consumable in windows 32/64 bit systems |

**Your application is optimised. Only the files of /dist folder are included in the executable.**

## Use NodeJS Native libraries

Actually Angular-Cli doesn't seem to be able to import nodeJS native libs or electron libs at compile time (Webpack error). This is (one of) the reason why webpack.config was ejected of ng-cli.
If you need to use NodeJS native libraries, you **MUST** add it manually in the file `webpack.config.js` in root folder :

```javascript
  "externals": {
    "electron": 'require(\'electron\')',
    "child_process": 'require(\'child_process\')',
    "fs": 'require(\'fs\')'
    ...
  },
```

Notice that all NodeJS v7 native libs are already added in this sample. Feel free to remove those you don't need.

## Browser mode

Maybe you want to execute the application in the browser (WITHOUT HOT RELOAD ACTUALLY...) ? You can do it with `npm run start:web`.  
Note that you can't use Electron or NodeJS native libraries in this case. Please check `providers/electron.service.ts` to watch how conditional import of electron/Native libraries is done.

## Execute E2E tests

You can find end-to-end tests in /e2e folder.

You can run tests with the command lines below : 
- **in a terminal window** -> First, start a web server on port 4200 : `npm run start:web`  
- **in another terminal window** -> Then, launch Protractor (E2E framework): `npm run e2e`

# Contributors 

[<img alt="Maxime GRIS" src="https://avatars2.githubusercontent.com/u/10827551?v=3&s=117" width="117">](https://github.com/maximegris) |
:---:
|[Maxime GRIS](https://github.com/maximegris)|

[build-badge]: https://travis-ci.org/maximegris/angular-electron.svg?branch=master
[build]: https://travis-ci.org/maximegris/angular-electron.svg?branch=master
[dependencyci-badge]: https://dependencyci.com/github/maximegris/angular-electron/badge
[dependencyci]: https://dependencyci.com/github/maximegris/angular-electron
[license-badge]: https://img.shields.io/badge/license-Apache2-blue.svg?style=flat
[license]: https://github.com/maximegris/angular-electron/blob/master/LICENSE.md
[prs-badge]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square
[prs]: http://makeapullrequest.com
[donate-badge]: https://img.shields.io/badge/$-support-green.svg?style=flat-square
[donate]: https://www.paypal.me/maximegris/10
[github-watch-badge]: https://img.shields.io/github/watchers/maximegris/angular-electron.svg?style=social
[github-watch]: https://github.com/maximegris/angular-electron/watchers
[github-star-badge]: https://img.shields.io/github/stars/maximegris/angular-electron.svg?style=social
[github-star]: https://github.com/maximegris/angular-electron/stargazers
[twitter]: https://twitter.com/intent/tweet?text=Check%20out%20angular-electron!%20https://github.com/maximegris/angular-electron%20%F0%9F%91%8D
[twitter-badge]: https://img.shields.io/twitter/url/https/github.com/maximegris/angular-electron.svg?style=social
