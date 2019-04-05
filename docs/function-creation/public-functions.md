# Public and Private Functions Overview

## Private Functions

Upon it's creation (running `bantam init` with the Bantam CLI), a function is initially set to private.

```
{
  "name": "@bundle/functionName",
  "version": "1.1.26",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "bantam": {
    "public": false
  },
  "author": "me",
  "license": "ISC",
  "private": true,
  "dependencies": {}
}
```

You can freely test and publish your functions without making them `PUBLIC`. To test a function locally use the Bantam CLI command `bantam test` within the directory of a function. Your are also able to incorporate your functions within your own projects or client work.

## Public Functions

If you are building or have a bundle of functions that you would like to make public for anyone integrated with Bantam to use. To publish a function to the masses, in the Bantam Config object in the function's `package.json`, simply add `"bantam": { "public": true }` to the `bantam` data object.

To publish a public function, you must have the pricing, memory, timeout, and public price setup. For more information on how to do that. Checkout the [pricing docs](../function-creation/pricing.md);

For more information about how to monetize your functions, check out our [docs here](../function-creation/making-money.md)

To provide other users the ability to 'try-out' your functions, check out our [examples docs here](../function-creation/examples.md)

```
{
  "name": "@bundle/functionName",
  "version": "1.1.26",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "bantam": {
    "public": true,
    "memory": 256,
    "timeout": 30,
    "publicPrice": 0.05
  },
  "author": "me",
  "license": "ISC",
  "private": true,
  "dependencies": {}
}
```
