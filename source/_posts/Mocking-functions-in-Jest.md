---
title: Mocking functions in Jest
date: 2017-04-02 21:48:55
tags:
---

[Jest](https://github.com/facebook/jest) is my test runner of choice for testing React based JavaScript.

#### Creating mocks

Here are some functions and patterns provided by Jest to mock out functions and modules:

1. <b>jest.fn(</b>__implementation__<b>)</b>

  Returns a new, unused mock function. Optionally takes a mock implementation.
  ```
  const myFunc = jest.fn(() => true);
  ```

2. <b>jest.mock(</b>__moduleName, factory, options__<b>)</b>

  Mocks a module with an auto-mocked version when it is being required.
  ```
  jest.mock('../moduleName', () => {
    return jest.fn(() => 42);
  });
  const moduleName = require('../moduleName');
  ```
  This runs the function specified as second argument to `jest.mock`.

3. <b>jest.spyOn(</b>__object, methodName__<b>)</b>

  Creates a mock function similar to jest.fn but also tracks calls to object[methodName]. Returns a Jest mock function.
  ```
  const spy = jest.spyOn(video, 'play');
  expect(spy).toHaveBeenCalled();
  ```

#### Jest auto mocking

Jest auto mocks **require** file syntax

If you need to test the actual files then you need to execute:
```
jest.dontMock('../myFile.js');
```

Note that it does not auto mock **ES6 imports** though!

If you wish to mock import modules, one option is:
```
import * as myModule from '../myModule.js';
let getData = spyOn(myModule, "getData")
```
This mocks myModule and tracks calls to getData function

Or using **jest.fn()**:

```
import * as myModule from '../myModule';
// getData is a named export
myModule.getData = jest.fn();
// getData is the default export
myModule.default = jest.fn();
```

#### Mock promise

You'll occasionally need to make a mock return a promise

This is easy:

```
myFunction: jest.fn().mockImplementation(() =>
  Promise.resolve(),
)
```

Note that **mockFn.mockImplementation(__fn__)** accepts a function that should be used as the implementation of the mock. The mock itself will still record all calls that go into it.
The only difference is that the implementation will also be executed when the mock is called.


#### And finally

If you wish to mock out an external node_module which is imported, use:
```
jest.mock('react-highcharts');
```
