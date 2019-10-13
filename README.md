## Let's build Youtube Music Desktop App 

We all love music and we all have used Youtube to find good music, but the problem is that even though Youtube is so popular, there isn't any desktop app for Youtube while its competitors like Spotify or Pandora has full fledged desktop apps. 

So, today we will build a desktop app for Youtube using [Electron](https://electronjs.org/) which is a cross platform framework to build desktop apps using web technologies such as javascript, html and css.

We will use Electron to build the app and then port it to Mac, Linux and Windows.

[I have also added a github repository to help you along the way. Find it here.](https://github.com/navi25/LearnStep-BuildYoutubeApp)


### Electron Overview

[Electron](https://electronjs.org/) is built and open sourced by Github. It provides javascript runtime with rich native (Operating system) APIs and thus takes care of the hard part and lets the developer focus on the core of their application. It can be thought of as Node.js variant focused on desktop application. It is powered by chromium engine and thus each application of electron is actually a self contained minimal web browser. In a nutshell, desktop app development using electron is actually a NodeJs development with focus on desktop development.


### Setup and Install dependencies

Make sure [Node.js and npm](https://nodejs.org/en/) is installed. Create an empty directory - YourProject and run following commands from that folder:


```
npm init
```


And follow along, it will prompt you to enter a few details, just enter as per your liking and can also leave for default values. Once it's completed you will have following folder structure-


```
YourProject/
----- package.json
----- README.md
----- LICENSE
```


and your package.json would look something like as follows -


```
{
 "name": "learnstep-buildyoutubeapp",
 "version": "1.0.0",
 "description": "A minimal introductory tutorial for Electron by building a Youtube desktop app",
 "main": "index.js",
 "scripts": {
   "test": "echo \"Error: no test specified\" && exit 1"
 },
 "repository": {
   "type": "git",
   "url": "git+https://github.com/navi25/LearnStep-BuildYoutubeApp.git"
 },
 "keywords": [
   "Electron",
   "Desktop",
   "app",
   "Youtube"
 ],
 "author": "Navendra Jha",
 "license": "MIT",
 "bugs": {
   "url": "https://github.com/navi25/LearnStep-BuildYoutubeApp/issues"
 },
 "homepage": "https://github.com/navi25/LearnStep-BuildYoutubeApp#readme"
}
```


Now lets install electron by typing following command - 


```
npm install --save-dev electron
```


Our main entry point to the app is denoted by the "main" field in the package.json which in our case is "index.js". So let's create an index.js file in that folder. 


```
touch index.js

// Our folder structure now looks like as follows
YourProject/
----- package.json
----- README.md
----- LICENSE
----- index.js
----- package-lock.json
----- node_modules/
```



### Develop the app

Paste following in the index.js.


```
const { app, BrowserWindow } = require('electron')

function createWindow () {
   // Create the browser window.
   let win = new BrowserWindow({
       width: 800,
       height: 600,
       webPreferences: {
           nodeIntegration: true
       }
   });

   let ytMusicUrl = "https://music.youtube.com";

   // and load the youtube music url.
   win.loadURL(ytMusicUrl)
}

app.on('ready', createWindow)
```


Now, let's try to understand what is happening here.



1. First, we are importing **"app"** and **"BrowserWindow"** from electron. These two are one of the most essential native apis provided by electron.  
"**BrowserWindow**" provides a chromium browser window as clear from its name. It can be used to load an html file or load any url in it. For our case we will be loading Youtube Music url in it. [You can read more about it here. \
](https://electronjs.org/docs/api/browser-window) **"app"** provides the interface for the whole desktop app and gives hooks for various events such as "ready", "quit" etc. [You can read more about it here.](https://electronjs.org/docs/api/app) 

2. Let's write a function **"createWindow"** in which we will create our browser window and after creating it we will load the youtube music url in it. 

3. Finally we will use **"app"** api to call this function when "app" is ready.


### Run the app

Now go back to package.json and add following line under "scripts"


```
"scripts" : {

...

"start" : "electron ."

...

}
```


now go to the terminal and run "npm start". It will start the app and you will see the Youtube music desktop app.


### Publish app

Now lets publish app. For that we will use "electron-packager" which helps in packaging the app and publishing it.


```
npm install --save-dev electron-packager
```


And add following to "scripts"


```
"scripts" : {

...

"package-mac": "electron-packager . --overwrite --platform=darwin --arch=x64 --prune=true --out=release-builds",
"package-win": "electron-packager . electron-tutorial-app --overwrite --asar=true --platform=win32 --arch=ia32 --icon=assets/icons/win/btc.ico --prune=true --out=release-builds --version-string.CompanyName=CE --version-string.FileDescription=CE --version-string.ProductName=\"CryptoApp\"",
"package-linux": "electron-packager . electron-tutorial-app --overwrite --asar=true --platform=linux --arch=x64 --icon=assets/icons/png/btc.ico --prune=true --out=release-builds"

...

}
```


Now go ahead and run the corresponding command for your os in terminal. For mac, we will do following


```
npm run package-mac
```


Now you can see the app for mac in the **release-builds** folder.

Well that's it. You have built a fully functional Youtube Music desktop app. This also gave you an introduction to Electron framework and as you can already see, it's essentially a nodejs development and so the scope is limitless. 

Happy Coding!

## LearnSteps

LearnSteps is a blog about technology, learning, mistakes, 
learning from mistakes, best practices, trending technologies and a whole lot more.
Subscribe to it at [learnsteps.com](https://learnsteps.com)

