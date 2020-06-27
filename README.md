
# TypeScript Setup with Node and Express by Traversy media

[TypeScript Setup with Node and Express | Traversy Media](https://youtu.be/zRo2tvQpus8)

## Some notes

`npm install -g typescript`
`tsc --init` to create tsconfig.json

Make changes (uncomment and update as needed) to tsconfig.json:

* Change "target" from "es5" to "es6" to get const instead of var, arrow functions, etc
* Change "outDir" from "./" to "./dist"
* Change "rootDir" from "./" to "./src"
* uncomment "moduleResolution": "node"

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "moduleResolution": "node",
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
  ```

Now move the app.ts file into /src.
`tsc` will now create the js file and put it in /dist.

`npm init` to get a package.json

`npm i express` to get express installed

Install your dev dependencies
`npm i -D typescript ts-node nodemon @types/node @types/express`

Add into your package.json file in scripts:

```json
  "scripts": {
    "start": "node dist/app.js",
    "dev": "nodemon src/app.ts",
    "build": "tsc -p ."
  },
```

In app.ts, get express started:

```js
import express from 'express';

const app = express();

app.get('/', (req, res) => {
  res.send('Hello');
});

app.listen(5000, () => console.log('Server running'));

```

Now go to command line and do `npm run dev` and it'll show server running. Open browser and navigate to <http://localhost:5000/> and you'll see Hello

To change the above to actually be TypeScript:

```ts
import express, { Application, Request, Response, NextFunction } from 'express';

const app: Application = express();

app.get('/', (req: Request, res: Response, next: NextFunction) => {
  res.send('Hello');
});

app.listen(5000, () => console.log('Server running'));

```

`npm run build` compiles your javascript into the app.js file which at this point now looks like this:

```js
"use strict";
var __importDefault = (this && this.__importDefault) || function (mod) {
    return (mod && mod.__esModule) ? mod : { "default": mod };
};
Object.defineProperty(exports, "__esModule", { value: true });
const express_1 = __importDefault(require("express"));
const app = express_1.default();
const add = (a, b) => a + b;
app.get('/', (req, res, next) => {
    console.log(add(5, 5));
    res.send('Hello');
});
app.listen(5000, () => console.log('Server running'));
```

When you're all done there, `npm start` is where you see it in "production mode" where it's using the app.js file instead of the app.ts file. Cool!
