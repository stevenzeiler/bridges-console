# Bridges Console

An embeddable REPL for Node.js: a "Rails console for Node". Put your classes in global scope, call `start()`, and poke at your app interactively.

> **Status: dormant since 2014.** Written by Steven Zeiler on 2014-12-11 (v1.0.0, two commits) for gatewayd and the "Bridges" application framework, during his 2014 Ripple Labs era. It uses `gulp-6to5` (the early name of Babel) and 2014-era dependencies, and has not been run on a current Node in this pass. Treat it as a reference.

## Install

    npm install --save bridges-console

## Usage

Globals set before the console starts are available at the prompt:

    var Console = require('bridges-console');

    global.MyApp = {
      database: { connected: false, type: 'postgres' },
      config: { version: '1.0.1' }
    };

    var myAppConsole = new Console();
    myAppConsole.start();

Then, at the prompt:

    console> MyApp.config.version;
    '1.0.1'

Type `exit` to leave.

### Options

    new Console({ loadDirectories: ['/path/to/models'], prompt: 'myapp' });

- `loadDirectories`: array of directory paths. Every file is loaded with [require-all-to-camel](https://github.com/stevenzeiler/require-all-to-camel), and each export is made a global named after the file, converted from snake case to camel case with the first letter capitalised (`payment_method.js` becomes `PaymentMethod`).
- `prompt`: the prompt name (default `console`).

The console also puts `_` (lodash) and `Promise` (bluebird) in global scope.

## Configuration

- `GATEWAYD_PATH`: used only by `test/gatewayd.js`, which loads gatewayd's models. Set it to your gatewayd checkout.

## How it works

`src/console.js` wraps Node's `repl` module with `useGlobal: true`. `src/index.js` adds lodash, bluebird and the `exit` command. Source is ES6 compiled to `build/` by gulp (`gulp-6to5`); `build/` is committed and is what `main` points to.

## Scripts

- `npm run console` starts the REPL from `build/index.js`.
- `npm test` runs `node test/basic.js`, which loads the sample models in `test/models/` and opens a prompt (it is a demo, not an assertion test). Not run in this pass.
- `test/gatewayd.js` needs `GATEWAYD_PATH`.

## Status

See [docs/STATUS.md](docs/STATUS.md). License: ISC (see [LICENSE](LICENSE)).
