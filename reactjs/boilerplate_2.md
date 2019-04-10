# React Setup

```bash
npm i react react-dom
```

***`src/client/app.js`***

```javascript
import React, {Component} from 'react'
export default class App extends Component {
    render() {
        return <div>Welcome to React Boilerplate App</div>
    }
}
```

***`src/client/index.js`***

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import App from './app'
ReactDOM.render(<App />, document.getElementById('root'))
```

# Babel React

```bash
npm install --save-dev babel-preset-react
```

***`.babelrc`***

```json
{
  "presets": ["env", "react"]
}
```

# Load Script in HTML

***`src/client/index.html`***

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React Boilerplate</title>
</head>
<body>
    <div id="root"></div>
    <script src="index.js"></script>
</body>
</html>
```

# Run Server

***`package.json`***

```json
"scripts": {
    "build-babel": "npm run build-babel-server && npm run build-babel-client",
    "build-babel-server": "babel src/server --out-dir ./dist",
    "build-babel-client": "babel src/client --copy-files --out-dir ./dist/public",
    "start": "node ./dist/index.js",
    "test": "jest ./src"
  }
```

# Webpack

```bash
npm i webpack@^3
```

***`webpack.config.js`***

```javascript
let path = require('path');
const client = {
    entry: {
        'client': './src/client/index.js'
    },
    target: 'web',
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist/public')
    }
};
const server = {
    entry: {
        'server': './src/server/index.js'
    },
    target: 'node',
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist')
    }
};
module.exports = [client, server];
```

# Babel Loader

```bash
npm install babel-loader --save-dev
```

***`webpack.config.js`***

```javascript
const path = require('path');
const moduleObj = {
    loaders: [
        {
            test: /\.js$/,
            exclude: /node_modules/,
            loaders: ["babel-loader"],
        }
    ],
};
const client = {
    entry: {
        'client': './src/client/index.js',
    },
    target: 'web',
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist/public')
    },
    module: moduleObj
};
const server = {
    entry: {
        'server': './src/server/index.js'
    },
    target: 'node',
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist')
    },
    module: moduleObj
}
module.exports = [client, server];
```

# Excluding Files

```bash
npm i webpack-node-externals --save-dev
```

***`webpack.config.js`***

```javascript
let path = require('path');
let nodeExternals = require('webpack-node-externals');
const moduleObj = {
    loaders: [
        {
            test: /\.js$/,
            exclude: /node_modules/,
            loaders: ["babel-loader"],
        }
    ],
};
const client = {
    entry: {
        'client': './src/client/index.js',
    },
    target: 'web',
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist')
    },
    module: moduleObj
};
const server = {
    entry: {
        'server': './src/server/index.js'
    },
    target: 'node',
    output: {
        filename: '[name].js',
        path: path.resolve(__dirname, 'dist')
    },
    module: moduleObj,
    externals: [nodeExternals()]
}
module.exports = [client, server];
```

# Update Build Command

***`package.json`***

```json
"scripts": {
    "build": "webpack",
    "build-babel": "npm run build-babel-server && npm run build-babel-client",
    "build-babel-server": "babel src/server --out-dir ./dist",
    "build-babel-client": "babel src/client --copy-files --out-dir ./dist/public",
    "start": "node ./dist/server.js",
    "test": "jest ./src"
  }
```

# Build Clean

```bash
npm install rimraf
```

***`package.json`***

```json
"scripts": {
...
"clean": "rimraf dist node_modules",
...
}
```

# Clean Build with Webpack

```bash
npm run clean
npm install
npm run build
```

# HTML Webpack Plugin

```bash
npm i html-webpack-plugin --save-dev
```

***`webpack.config.js`***

```javascript
const HtmlWebPackPlugin = require('html-webpack-plugin')
const client = {
  entry: {
    'client': './src/client/index.js'
  },
  target: 'web',
  output: {
    filename: '[name].js',
    path: path.resolve(__dirname, 'dist/public')
  },
  module: moduleObj,
  plugins: [
    new HtmlWebPackPlugin({
      template: 'src/client/index.html'
    })
  ]
}
```

***`src/client/index.html`***

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React Boilerplate</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
```

# [SOURCE](https://medium.freecodecamp.org/how-to-build-your-own-react-boilerplate-2f8cbbeb9b3f)