# Folder Structure

```
root
    |--src
        |--client
        |--server
    |--.gitignore
```

# Node Package Manager

```bash
npm init
```

# Static Content

***`src/client/index.html`***

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>React Boilerplate</title>
</head>
<body>
    <div id="root">
        Welcome to React Boilerplate!
    </div>
</body>
</html>
```

# Express Web Server

```bash
npm install express
```

***`src/server/web.server.js`***

```javascript
const express = require('express')
export default class WebServer {
  constructor () {
    this.app = express()
    this.app.use(express.static('dist/public'))
  }
  start () {
    return new Promise((resolve, reject) => {
      try {
        this.server = this.app.listen(3000, function () {
          resolve()
        })
      } catch (e) {
        console.error(e)
        reject(e)
      }
    })
  }
  stop () {
    return new Promise((resolve, reject) => {
      try {
        this.server.close(() => {
          resolve()
        })
      } catch (e) {
        console.error(e.message)
        reject(e)
      }
    })
  }
}
```

# Startup File

***`src/server/index.js`***

```javascript
import WebServer from './web.server'
let webServer = new WebServer();
webServer.start()
  .then(() => {
    console.log('Web server started!')
  })
  .catch(err => {
    console.error(err)
    console.error('Failed to start web server')
  });
```

# Babel

```bash
npm i babel-cli babel-preset-env --save-dev
```

***`.babelrc`***

```json
{
  "presets": ["env"]
}
```

# Build Commands

***`package.json`***

```json
"scripts": {
    "build": "npm run build-server && npm run build-client",
    "build-server": "babel src/server --out-dir ./dist",
    "build-client": "babel src/client --copy-files --out-dir ./dist/public",
    "start": "node ./dist/index.js"
}
```

# Starting up

```bash
npm run build
npm start
```

# Test Harness: Jest

```bash
npm i jest --save-dev
```

# Unit Tests

***`src/server/web.server.test.js`***

```javascript
import WebServer from './web.server'
describe('Started', () => {
  let webServer = null
  beforeAll(() => {
    webServer = new WebServer()
  })
  test('should start and trigger a callback', async () => {
    let promise = webServer.start()
    await expect(promise).resolves.toBeUndefined()
  })
  test('should stop and trigger a callback', async () => {
    let promise = webServer.stop()
    await expect(promise).resolves.toBeUndefined()
  })
})
```

# Test Command

***`package.json`***

```json
"scripts": {
...
    "test": "jest ./src"
...
}
```

```bash
npm test
```
