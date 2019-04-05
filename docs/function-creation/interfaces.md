# Interfaces

Interfaces allow you to redirect a user from the function dashboard to a URL you own and authenticate that user with Bantam. Providing a `webInterface` config URL will create a `Open in Interface` tab on the function dashboard.

This allow you to extend your function monetization from within your own platform.

Example interfaces include the built in [@simple/log](https://bantam.io/functions/@simple/log) or [@metrics/running-window](https://bantam.io/functions/@metrics/running-window).

## How to create an interface

### Step 1: Add your external URL to the `package.json` bantam object.

This is the URL that the "Open in Interface" button will redirect the user to.

```js
inside package.json...
  "bantam": {
    "webInterface": "https://runningwindow.bantam.io/dashboard",
  }
```

When the user is redirected, we provide a temporary token parameter to authenticate that user as seen below.

`https://runningwindow.bantam.io/dashboard?token=<SOME_TOKEN>`

### Step 2: Authenticate the user with the provided token

```js
bantam
  .run('@publishing/user-auth', {
    function: '@my-bundle/my-function',
    token: '<SOME_TOKEN>',
  })
  .then(
    userId => {
      // authorized as userId
    },
    e => {
      // unauthorized
    }
  );
```
