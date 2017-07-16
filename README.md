# This is a boilerplat on how to integrate Mocha/Chai/Enyzme in create-react-app project.

This project was bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app).

## Step 1: Create react project with create-react-app cli

```console
create-react-app react-mocha-boilerplate
cd react-mocha-boilerplate
```

## Step 2: Install Mocha/Chai/Enzyme

```console
npm run eject
npm install chai enzyme mocha react-addons-test-utils sinon --save-dev
npm install babel-preset-es2015 babel-preset-stage-2 --save-dev
```

## Step 3: Change the default test script in `package.json`

```json
......
  "scripts": {
    "test": "mocha --require ./testSetup.js --compilers babel-core/register ./test/*test.js",
    "test:watch": "npm test -- -w"
  },
......
```

## Step 4: Add a test configuration file `testSetup.js` under the project root folder

```javascript
'use strict';

import jsdom from 'jsdom';

global.document = jsdom.jsdom('<html><body></body></html>');
global.window = document.defaultView;
global.navigator = window.navigator;

function noop() {
  return {};
}

// prevent mocha tests from breaking when trying to require a css file
require.extensions['.css'] = noop;
require.extensions['.svg'] = noop;
```

## Step 5: Add test folder and a test file (`./test/demotest.test.js`)

```javascript
import React from 'react'
import { shallow } from 'enzyme'
import { expect } from 'chai'
import App from '../src/App'

const wrapper = shallow(<App />);

describe('(Component) App', () => {
  it('renders...', () => {
    expect(wrapper).to.have.length(1);
  });
});
```

## Step 6: Add a `.babelrc` file, and set the preset

```json
{
    "presets": ["es2015", "stage-2", "react"]
}
```

## Step 7: Run the test under project root path

```console
npm run test
```