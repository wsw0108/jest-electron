# @wsw0108/jest-electron

> Easiest way to run jest unit test cases in electron.

When we run unit test in Jest, it is actually running in the node environment, or virtual browser environment(e.g. `JSDOM`) mocked by NodeJS. Sometimes we need a lot of [Jest mocks](https://github.com/jest-community/awesome-jest#mocks) for running code with no throw, such as: jest-canvas-mock, jest-storage-mock, @jest/fake-timers and so on. This is solved by `Jest-Electron`.

[![Build Status](https://github.com/hustcc/jest-electron/workflows/build/badge.svg)](https://github.com/hustcc/jest-electron/actions)
[![npm](https://img.shields.io/npm/v/jest-electron.svg)](https://www.npmjs.com/package/jest-electron)
[![npm](https://img.shields.io/npm/dm/jest-electron.svg)](https://www.npmjs.com/package/jest-electron)


1. Technological ecology of `Jest`.
2. Complete and real `browser environment`.
3. `Multi-renderer` for running performance.
4. `Running and debug` is better then mock.


## Installation


 - Add into devDependencies

```bash
$ npm i --save-dev @wsw0108/jest-electron
```

 - Update Jest config

```diff
{
  "jest": {
+    "runner": "@wsw0108/jest-electron/runner",
+    "testEnvironment": "@wsw0108/jest-electron/environment"
  }
}
```

**Notice**: update the `runner` configure, not `testRunner`.



## Related

> Those will be helpful when run test case with `jest-electron`.

 - [jest-less-loader](https://github.com/hustcc/jest-less-loader): Run test cases with import `less`, `css` code.
 - [jest-url-loader](https://github.com/hustcc/jest-url-loader): Run test cases with import `svg`, `png`, `jpg` or other url file..



## CI

> Run test cases with `jest-electron` for continuous integration.

 - **GitHub action**

Running on `macOS` will be ok.


```diff
- runs-on: ubuntu-latest
+ runs-on: macOS-latest
```


 - **travis**

Update `.travis.yml` with electron supported.
 
```diff
language: node_js
node_js:
  - "8"
  - "9"
  - "10"
  - "11"
  - "12"
+ addons:
+   apt:
+     packages:
+       - xvfb
+ install:
+   - export DISPLAY=':99.0'
+   - Xvfb :99 -screen 0 1024x768x24 > /dev/null 2>&1 &
+   - npm install
script:
  - npm run test
```

Depending on your executor, you might need to disable sandbox and shared memory usage:

```bash
export JEST_ELECTRON_STARTUP_ARGS='--disable-dev-shm-usage --no-sandbox'
npm run test
```

## Env

 - **debug mode**

Keep the electron browser window for debugging, set process env `DEBUG_MODE=1`.


```bash
DEBUG_MODE=1 jest
```

 - **additional startup arguments**

Run electron with arbitrary arguments.

```bash
JEST_ELECTRON_STARTUP_ARGS='--disable-dev-shm-usage'
```

Run electron with `--no-sandbox`, set process env `JEST_ELECTRON_STARTUP_ARGS='--no-sandbox'`.

```bash
JEST_ELECTRON_STARTUP_ARGS='--no-sandbox' jest
```


## License

MIT@[hustcc](https://github.com/hustcc).
