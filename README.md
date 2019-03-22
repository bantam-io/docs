# Bantam Developer Docs

- [Intro to Function Creation](#Intro-to-Function-Creation)
- [Responding with a URL](#Responding-With-A-URL)

## Intro to Function Creation

To make building functions easier use the bantam cli…

https://www.npmjs.com/package/@bantam-io/cli

You can install with `npm install -g @bantam-io/cli`

Then you can build/test/deploy functions, view their logs, etc from the command `bantam`.

But you’ll need to set up your authorization. First, setup your bantam account on https://bantam.io/ .
Once, you are logged in, you can navigate to the “Keys” tab on the left side to get the API and secret.
Then you can authenticate by running `bantam configure` on your commandline.

Simple docs here: https://www.npmjs.com/package/@bantam-io/cli or run `bantam --help`.

_Creating a new function_ - `bantam init`

It will ask for a function name. Our functions are formatted like this `@bundle-name/function-name`. Even further, our functions can have “methods” - `@bundle-name/function-name/method-name`. A method is basically an option on the same function/lambda.

Here is the example code for a function:

```js
const bantamHandler = require('@bantam-io/handler').handler;

exports.handler = bantamHandler({})
  .on('default', (userId, args, callback) => {
    console.log('default | %j', args);
    callback(null, 'ALL DONE');
  })
  .on('sampleMethodOne', (userId, args, callback) => {
    console.log('sampleMethodOne | %j', args);
    callback(null, 'ALL DONE');
  })
  .on('sampleMethodTwo', (userId, args, callback) => {
    console.log('sampleMethodTwo | %j', args);
    callback(null, 'ALL DONE');
  });
```

You’ll see three `on` events. Let’s say my function where `@test/sample`. If someone were to do `bantam.run('@test/sample', { key: 'value' })`, the `.on('default' ...` would be called (no method). If you were to call `bantam.run('@test/sample/sampleMethodOne', { key: 'value' })`, the `on('sampleMethodOne', ...` would be called.

One more thing to note: the `userId` is the ID of the user who called the function. The `args` is just the args they pass.

_Testing a function locally_

If you’re in the directory of your fn, run `bantam test --input ./path/to/file.json`, where the input file is your arguments to the function. You can run `bantam test -m methodName --input ./file.json` if testing a method.

_Publishing functions_

• Step 1. Make sure your README.md file is accurate.
• Step 2. Make sure you increment your `version` number in package.json (`1.0.1`, `1.0.2`, etc).
• Step 3. `bantam publish`

# Responding with a URL

Say for example you want someone to go directly to a BantamURL and have it show an image. You may not want to run JavaScript with a promise, get the response, and then put the response in an the `src` tag for an `img`. You may instead just want to put a URL as the `src` that runs the bantam function and then responds with an image.

Great.

As a function developer, you just respond like this:

```js
cb(null, {
  proxyResponse: {
    statusCode: 302,
    headers: {
      Location: url,
    },
    body: '',
  },
});
```

If they use `bantam.run` instead of going to the `bantam.url`, that's okay - we figure that out and just respond with the URL as the result.
