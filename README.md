# MetaMask Test Dapp

This is a simple test dapp for use in MetaMask e2e tests and manual QA.

Currently hosted [here](https://metamask.github.io/test-dapp/).

## Usage

If you wish to use this dapp in your e2e tests, install this package and set up a script of e.g. the following form:

```shell
static-server node_modules/@metamask/test-dapp/dist --port 9011
```

The main page of the test dapp includes a simple UI featuring buttons for common dapp interactions.

There is a second page (`request.html`) that allows making requests directly to the provider using query parameters. This provides a simple way of testing RPC methods using an in-page provider.

It can be used by navigating to `/request.html?method=${METHOD}&params=${PARAMS}` (e.g. `/request.html?method=eth_getLogs&params=[{ "address": "0x0000000000000000000000000000000000000000" }]`). The page will make a request with the given RPC method and parameters using `ethereum.request`, and report the result as plain text.

## Simple Usage

```shell
yarn start
```

## Contributing

### Setup

- Install [Node.js](https://nodejs.org) version 16
  - If you are using [nvm](https://github.com/creationix/nvm#installation) (recommended) running `nvm use` will automatically choose the right node version for you.
- Install [Yarn v1](https://yarnpkg.com/en/docs/install)
- Run `yarn setup` to install dependencies and run any required post-install scripts
  - **Warning:** Do not use the `yarn` / `yarn install` command directly. Use `yarn setup` instead. The normal install command will skip required post-install scripts, leaving your development environment in an invalid state.

### Testing and Linting

Run `yarn lint` to run the linter, or run `yarn lint:fix` to run the linter and fix any automatically fixable issues.

This package has no tests.

### Deploying

After merging or pushing to `main`, please run `yarn deploy` in the package root directory if the contents of the `dist/` directory have changed.

### Development

#### Elements Must Be Selectable by XPath

All HTML elements should be easily selectable by XPath.
This means that appearances can be misleading.
For example, consider this old bug:

```html
<button
  class="btn btn-primary btn-lg btn-block mb-3"
  id="approveTokensWithoutGas"
  disabled
>
  Approve Tokens Without Gas
</button>
```

This appears on the page as `Approve Tokens Without Gas`. In reality, the value included the whitespace on the second line, and caused XPath queries for the intended value to fail.
