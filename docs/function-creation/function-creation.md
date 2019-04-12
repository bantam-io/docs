# Function Creation

## Creating functions with the Bantam CLI

The Bantam CLI can be found at [https://www.npmjs.com/package/@bantam-io/cli](https://www.npmjs.com/package/@bantam-io/cli)

The primary use of this CLI is to create, test and publish your own functions. Created functions can be for [private or public](public-functions.md) use and can even be monetized (more info on that [here](making-money.md)).

> Note: You will need to [create an account](https://bantam.io/landing/bundle/@images) in order to test or publish a function.

## Developing Functions - Bantam CLI Walkthrough

### Step 1: Download and install the Bantam CLI globally

```
npm install -g @bantam-io/cli
```

### Step 2: Configure and login to Bantam

This step will prompt you for your `email`, `password`, and your `SECRET KEY`

```
bantam configure
```

### Step 3: Create a local directory, init and write a new function

This step will prompt you for the `@bundle` and `function name`. Our functions are formatted like this `@bundle-name/function-name`. Even further, our functions can have `methods` - `@bundle-name/function-name/method-name`. A method is basically an option on the same function.

> Be sure to use a bundle identifier that you own and have created through the dashboard [here](https://bantam.io/develop)

```
cd my-project/
bantam init
```

Here is some example code for a function inside of the `index.js` file:

```javascript
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

You’ll see three on events. Let’s say my function where @test/sample. If someone were to do `bantam.run('@test/sample', { key: 'value' })`, the `.on('default' ...` would be called (no method). If you were to call `bantam.run('@test/sample/sampleMethodOne', { key: 'value' })`, the `on('sampleMethodOne', ...` would be called.

> One more thing to note: the userId is the ID of the user who called the function. The args is just the args they pass.

### Step 4: Test your function locally

If you’re in the directory of your function, run `bantam test --input ./path/to/file.json`, where the input file is your arguments to the function. You can run `bantam test -m methodName --input ./file.json` if testing a method.

```
cd my-project/@<bundle_identifier>/<function_name>/<method_name>
bantam test
```

### Step 5: Publish your function

> Everytime you run bantam publish we overwrite your current function. You also need to make sure to update the version of your function prior to publishing. As you are the owner of the function, it is up to you to manage the versioning.

> `To do this, change the value of "version" in the package.json file.`

```
bantam publish
```

### Step 6: Make your function PUBLIC

Now that you have a published function, you should it in the functions tab of the dashboard.

Click through to your new function's page, and navigate to the 'administration' tab on left-hand menu. There your can allow your function to be published publicly. This will require your to re-publish your function.

## Bantam CLI Usage

Prompt format:

```
bantam [command][options]
```

> Remember to always be in your function's directory when running and function related commands.

Commands:

```
configure [options]        Configure bantam, particularly with authentication
init [options]             Init a new function
logs [options] <function>  Get logs for a function you developed
me [options]               Check who you are logged in as
publish [options]          publish function
run [options] <function>   Run function
test [options]             test function
```

Options:

```
-v, --version              output the version number
-h, --help                 output usage information
```

## Function Monitoring

We provide some monitoring. For more advanced monitoring, we recommend [iopipe.com](https://www.iopipe.com/). You can easily integrate with the bantam handler like this:

```
exports.handler = bantamHandler({
  ioPipeKey: 'YOUR_IO_PIPE_KEY'
})
.on('default', (userId, args, callback) => {
  callback(null, args);
})
```
