# Public and Private Functions

Upon a functions creation (running `bantam init` with the Bantam CLI), the function is set to private (`"bantam": { "public": false }`). <i>Note: The top level `"private"` value, it is unrelated to Bantam. </i>

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
    "memory": 128,
    "timeout": 5,
    "public": false
  },
  "author": "me",
  "license": "ISC",
  "private": true,
  "dependencies": {}
}
```
By keeping your function non-public, only function calls using your API keys can call the function. Therefore, you can test, publish and incorporate your function into your projects or client work without making your function `public`.

## Public Functions

To publish a function for other developers to consume requires 3 steps. The extra steps are to protect you from mistakenly making a function avaiable for public use.

1. `publish` the function to Bantam
2. 'Enable Public Deploy' via the Dashboard
3. Re-publish the function as public

#### 1. Publish the function:

`publish` the function to Bantam. [Additional info](../function-creation/function-creation.md#step-5-publish-your-function)

#### 2. Enable Public Deploy

Once your function is deployed to bantam, login to Batam.io. Click through to your new function's page, and navigate to the 'administration' tab on left-hand menu, then click 'settings'. There your can allow your function to be published publicly, by clicking 'Enable Public Deploy'.

NOTE: If you are unable to find your function, review step #1.  Do any errors appear in the console?

#### 3. Re-publish the function.

Update `package.json`, by changing `"bantam": { "public": false }` to `"bantam": { "public": true }`and adding `"bantam": { "publicPrice": x.xxx }`, see [pricing docs](../function-creation/pricing.md) to see your costs structure. Then redeploy (step #1). 

The result should look something like this:


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
For more information about how to monetize your functions, check out our [docs here](../function-creation/making-money.md)

To provide other users the ability to 'try-out' your functions, check out our [examples docs here](../function-creation/examples.md)
