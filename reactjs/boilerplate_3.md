# Enzyme Setup

```bash
npm i --save-dev enzyme enzyme-adapter-react-16 react-test-renderer
```

***`src/enzyme.setup.js`***

```javascript
import Enzyme from 'enzyme'
import Adapter from 'enzyme-adapter-react-16'
Enzyme.configure({
    adapter: new Adapter()
})
```

***`package.json`***

```json
{
...
"jest": {
    "setupTestFrameworkScriptFile": "./src/enzyme.setup.js"
  }
...
}
```

# React Component Test

***`package.json`***

```javascript
import App from './app'
import React from 'react'
import {shallow} from 'enzyme'
describe('App', () => {
  test('should match snapshot', () => {
    const wrapper = shallow(<App/>)
    expect(wrapper.find('div').text()).toBe('Welcome to React Boilerplate App')
    expect(wrapper).toMatchSnapshot()
  })
})
```