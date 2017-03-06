# react-project-template
The following instructions demonstrate how to set up a **React** project using

- **TypeScript**
- **Redux**
- **Jest**

## Inspiration
Inspiration and instruction for this project was taken from the following blog posts and documention.

#### Blog Posts and Documentation
- [https://scotch.io/tutorials/setup-a-react-environment-using-webpack-and-babel](https://scotch.io/tutorials/setup-a-react-environment-using-webpack-and-babel)
- [https://www.typescriptlang.org/docs/handbook/react-&-webpack.html](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)
  - Some parts out of date: [https://github.com/Microsoft/TypeScript/issues/13873](https://github.com/Microsoft/TypeScript/issues/13873)

#### Documentation
- [https://webpack.github.io/docs/webpack-dev-server.html](https://webpack.github.io/docs/webpack-dev-server.html)

## File Structure
This project uses the following file structure

```
.
|-- index.html
|-- client
    |-- index.js
    |-- components
|-- dist
    |-- bundle.js
|-- package.json
|-- node_modules
```

where the above directories and files correspond to the following:

- `index.html` - html page served up to the client
- `client/` - javascript source code
- `client/index.js` - entry point for the javascript code
- `dist/` - output folder for the compiled javascript code
- `dist/bundle.js` - transpiled javascript application

## Step 1 - set up [yarn](https://yarnpkg.com/en/) or [npm](https://www.npmjs.com/)
You can choose to manage dependencies using either yarn or npm. As of early 2017 it's not clear if yarn will become the defacto standard, but it seems to be gaining popularity. These instructions will use `yarn`, but you can also use `npm` with minimal tweaks to the following instructions.

You can find instructions for installing yarn [here](https://yarnpkg.com/lang/en/docs/install/)

Create a new directory, `cd` into it and initialize your project via:
```
yarn init
```

This will take ask your a series of questions, and will generate a `package.json` file based on how you answer them. You can always update the `package.json` file in the future, so don't feel like you have to configure everything correctly out of the box. 


## Step 2. Install Dependencies

#### Webpack(https://webpack.js.org/)
We we are going to use webpack to manage our code. First, install webpack, webpack-dev-server via the following command.

```
yarn add webpack webpack-dev-server

yarn add react react-dom @types/react @types/react-dom

yarn add typescript awesome-typescript-loader source-map-loader --dev
```

#### React
We want to install React for use with TypeScript. To do this run


```
yarn add react react-dom @types/react @types/react-dom
```

#### TypeScript
Lastly, we need to install TypeScript

```
yarn add typescript awesome-typescript-loader --dev
```

We specified `awesome-typescript-loader` which we will use as our TypeScript loader. The [TypeScript docs](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html) seem to recommend using `awesome-typescript-loader`, but also also mention [`ts-loader`](https://github.com/TypeStrong/ts-loader) as an alternative. I have not used it, but it may be worth investigating.

Installing the above dependencies will create a `node_modules` directory, `yarn.lock` file, and a `package.json` file including all of the dependencies we have installed thus far.

## Step 2. Configuration Files
We need to add configuration files for webpack and TypeScript.

#### Webpack Configuration
Create a `webpack.config.js` file, and update it to look something like this.

```
const path = require('path');
module.exports = {
  entry: './client/index.tsx',
  output: {
    path: path.resolve('dist'),
    publicPath: "/dist/",
    filename: 'bundle.js'
  },
  devtool: "source-map",
  resolve: {
    // Add '.ts' and '.tsx' as resolvable extensions.
    extensions: [".webpack.js", ".web.js", ".ts", ".tsx", ".js"] 
  },
  module: {
    loaders: [
      { test: /\.tsx$/, loader: 'awesome-typescript-loader' },
    ],
  }
}
```

The `webpack.config.js` file defines the entry point for our javascript code to live in `./client/index.js`, and specifies that the compiled javascript be placed in `./dist/bundle.js`.

#### TypeScript Configuration
Create a TypeScript configuration file called `tsconfig.json` with the following contents:

```
{
  "compilerOptions": {
    "outDir": "./dist/",
    "sourceMap": true,
    "noImplicitAny": true,
    "module": "commonjs",
    "target": "es5",
    "jsx": "react"
  },
  "include": [
    "./client/**/*"
  ]
}
```

You can reference the [TypeScript docs](https://www.typescriptlang.org/docs/handbook/compiler-options.html) to understand the different `compilerOptions` and what they do. The above configuration should be enough to get you off the ground.

## 
