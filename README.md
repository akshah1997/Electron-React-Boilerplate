# Electron-React-Boilerplate
The boilerplate code to get you started on developing React based Electron applications

## Creating the environment for the app

Because we are using React, we'll start by creating React application and then add Electron to it.

Make sure you have [NodeJS](https://nodejs.org/en/download/) installed on your computer.
We'll start by using `create-react-app`

## Create React app using `create-react-app`

 To install `create-react-app` as global package, run the following command -

```bash
    $ npm install -g create-react-app
```

Create new React app and `cd` into it -
```bash
    $ create-react-app electron-react-boilerplate
    $ cd helloworld
```
Now we have the basic React app, lets run it using `start` script defined in `package.json` file -

```bash 
    $ npm start
```

This starts the new broswer window with the default React page.

### Install Electron

To install `Electron` package run the following command -

```bash
    $ npm install electron --save-dev
```

Make sure you add the `--save-dev` option. It will add the `Electron` dependency to the `package.json` file.

Open `package.json` file, you should see `Electron` package inside `devDependencies` section.

Add the following line to scripts section -

`"electron-start": "electron ."`

Add a top-level `main` property and point it to main `Electron` file -

`"main": "public/electron.js"`

The `package.json` file now looks like this -

```
{
  "name": "electron-react-boilerplate",  
  "version": "0.1.0",  
  "main": "public/electron.js",  
  "private": true,  
  "dependencies": {  
    "react": "^16.3.0",  
    "react-dom": "^16.3.0",  
    "react-scripts": "1.1.1"  
  },  
  "scripts": {  
    "start": "react-scripts start",  
    "build": "react-scripts build",  
    "test": "react-scripts test --env=jsdom",  
    "eject": "react-scripts eject",  
    "electron-start": "electron ."  
  },  
  "devDependencies": {  
    "electron": "^1.8.4"  
  }  
}   
```
### Creating `electron.js` File

Created the `electron.js` file insde the `public` folder.

It contains some of the Electron's event to control the application's life cycle.

### Running the application

Make sure React is still running in the background else run the following command -

```bash
    $ npm start
```

Run the following command to start your Electron application -

```bash 
    $ npm run electron-start
```


## Creating a stable development and build process

We need to add the following packages -
1. `electron-builder`
2. `wait-on`
3. `concurrently`

Run the following command to add these packages to our app -

```bash
    $ npm install electron-builder wait-on concurrently --save-dev
```

```bash
    $ npm install electron-is-dev --save
```

Add the following in the `scripts` section of `package.json` file -

`"electron-dev": "concurrently \"BROWSER=none npm run start\" \"wait-on http://localhost:3000 && electron .\""`

The following things happen when you excute the above command -
1. `concurrently` - runs following commands at the same time
2. `BROWSER=none npm run start` - starts React application and not allow browser to open React application
3. `wait-on http://localhost:3000 && electron .` - wait for the development server to start. Once up, it will start the Electron application.

Now can run the application using -

```bash
    $ npm run electron dev
```

### Create `build` script

Add the following in the `scripts` section of `package.json` file -

`"preelectron-pack": "npm build"`

`"electron-pack": "build -- em.main=build/electron.js"`

Next, we will have to specify the `build` property. This is because of a minor conflict between `create-react-app` and `electron-builder`. Both are using the `build` folder for a different purpose.

Add the following `build` section to the `package.json` file -

```
"build": {
    "appId": "com.mook",
    "files": [
      "build/**/*",
      "node_modules/**/*"
    ],
    "directories": {
      "buildResources": "assets"
    }
  }
 ```
  
We also need to add the `homepage` property to allow the packaged Electron app to find the JavaScript and CSS files -
 
`"hompage": "./"`
 
### Building the app
  
Run the following command -
  
```bash
    $ npm run electron-pack
```

When the script run is complete, you should see a new folder named `dist` in your project’s directory. You can find your packaged application in the folder named after your operating system. For example, Mac users will be able to find the packaged application `electron-react-boilerplate.app` in the `dist/mac` folder.

Excellent! All you need now is to start coding!
