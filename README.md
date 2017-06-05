# learning-typescript
## This repository server as a simple guide to Typescript


### This guide is still being developed

A step by step guide to setting up [Typescript](https://www.typescriptlang.org).

Install with npm
```bash
$ npm install -g typescript
$ npm install -g webpack
$ npm install -g ts-loader // links webpack to complie typescript
$ npm install -g jquery  // to use jquery in your project
$ npm install -g http-server // to have a local server run
```
==========

#### Configure [Typescript](https://www.typescriptlang.org)

1. Create new Typescript file **main.ts**:
```typescript
 class SweetSweetClass {
     constructor() { 
         console.log("Even sweeter")
     }
 }
 let basil = new SweetSweetClass()
 ```
 
 
2. Setup **tsconfig.json**:

```ljson
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
 ```
 
3. Run:

 ```bash
 $ tsc 
 $ tsc --watch
 ```
 
Notice that the directory dist and the file **main.js** were created.

4. Setup HTML Page:

```html
 <!DOCTYPE html>
 <html>
 <head>
     <title></title>
 </head>
 <body>
 <script src='/dist/main.js'></script>
 </body>
 </html>
 ```
 
5. Run:
```bash
 $ http-server -c-1
```
or
```bash
 $ http-server
```

Using the flag *-c-1* makes the browser never cache the files.

6. Open up the **Javascript** Console and find the statement "Even sweeter"

#### Run & Compile with Webpack

1. Setup **webpack.config.js**:

```javascript

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
 ```
 
2. Run webpack:

Non minified

``` bash
 $ webpack --watch
```
As minified

```bash
 $ webpack --watch --optimize-minimize
```

3. Add new [Typescript](https://www.typescriptlang.org) file called **getcoffee.ts**:

```javascript
 export class MustHaveCoffee {
     constructor() { 
         console.log("yeah me too!")
     }
 }
 ```
 
4. Open **main.ts**:

```typescript
 import {MustHaveCoffee} from "./getcoffee"

 class SweetSweetClass {
     constructor() { 
         console.log("Even sweeter")
     }
 }

 let basil = new SweetSweetClass()
 let coffee = new MustHaveCoffee()
 ```
 
5. Update **index.html**:

```html
 <!DOCTYPE html>
 <html>
 <head>
     <title></title>
 </head>
 <body>
 <script src='/dist/bundle.js'></script>
 </body>
 </html>
 ```
 
#### Include jQuery with Typings

1. Install **typings**:

```bash
 $ npm install typings -g
```

2. In your project, run:

 ```language-bash
 $ typings install dt~jquery --global --save
```

3. Run:
```bash
 $ typings install
```

4. Update **tsconfig.json**:

```json
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
 ```
 
5. Import jQuery in **main.ts**

```typescript
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
 ```
jQuery works!
