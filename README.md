# learning-typescript
This repository server as a simple guide to Typescript


This guide is still being developed

A step by step guide to setting up Typescript.

Install with npm

$ npm install -g typescript
$ npm install -g webpack
$ npm install -g ts-loader // links webpack to complie typescript
$ npm install -g jquery  // to use jquery in your project
$ npm install -g http-server // to have a local server run
==========

Configure Typescript

Create new Typescript file main.ts:

 class SweetSweetClass {
     constructor() { 
         console.log("Even sweeter")
     }
 }
 let basil = new SweetSweetClass()
Setup tsconfig.json:

 {
   "compilerOptions": {
     "module": "commonjs",
     "outDir": "dist/",
     "noImplicitAny": true,
     "removeComments": true,
     "preserveConstEnums": true
   },
   "include": [
     "*"
   ],
   "exclude": [
       "node_modules",
       "**/*.spec.ts"
   ]
 }
Run:

 $ tsc 
 $ tsc --watch
Notice that the directory dist and the file main.js were created.

Setup HTML Page:

 <!DOCTYPE html>
 <html>
 <head>
     <title></title>
 </head>
 <body>
 <script src='/dist/main.js'></script>
 </body>
 </html>
Run:

 $ http-server -c-1
or

 $ http-server
Using the flag -c-1 makes the browser never cache the files.

Open up the Javascript Console and find the statement "Even sweeter"

Run & Compile with Webpack

Setup webpack.config.js:

 var path = require('path');

 module.exports = {
   entry: './main.ts',
   resolve: {
     extensions: ['.webpack.js', '.web.js', '.ts', '.js']
   },
   module: {
     loaders: [
       { test: /\.ts$/, loader: 'ts-loader' }
     ]
   },
   output: {
     filename: 'bundle.js',
     path: path.resolve(__dirname, 'dist')
   }
 }
Run webpack:

Non minified

 $ webpack --watch
As minified

 $ webpack --watch --optimize-minimize
Add new Typescript file called getcoffee.ts:

 export class MustHaveCoffee {
     constructor() { 
         console.log("yeah me too!")
     }
 }
Open main.ts:

 import {MustHaveCoffee} from "./getcoffee"

 class SweetSweetClass {
     constructor() { 
         console.log("Even sweeter")
     }
 }

 let basil = new SweetSweetClass()
 let coffee = new MustHaveCoffee()
Update index.html:

 <!DOCTYPE html>
 <html>
 <head>
     <title></title>
 </head>
 <body>
 <script src='/dist/bundle.js'></script>
 </body>
 </html>
Include jQuery with Typings

Install typings:

 $ npm install typings -g
In your project, run:

 $ typings install dt~jquery --global --save
Run:

 $ typings install
Update tsconfig.json:

 {
   "compilerOptions": {
     "module": "commonjs",
     "outDir": "dist/",
     "noImplicitAny": true,
     "removeComments": true,
     "preserveConstEnums": true
   },
   "include": [
     "src/*",
     "typings/*"
   ],
   "exclude": [
       "node_modules",
       "**/*.spec.ts"
   ]
 }
Import jQuery in main.ts

 import * as $ from "jquery";
 import {MustHaveCoffee} from "./getcoffee"

 class SweetSweetClass {
     constructor() { 
         console.log("Even sweeter");
         $('body').css('background-color', 'red');
     }
 }

 let basil = new SweetSweetClass()
 let coffee = new MustHaveCoffee()
jQuery works!
