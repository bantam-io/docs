# Function Creation

## Creating functions with the Bantam CLI

The Bantam CLI can be found at https://www.npmjs.com/package/@bantam-io/cli

The primary use of this CLI is to create, test and publish your own functions. Created functions can be for [private or public](public-functions.md) use and can even be monetized (more info on that [here](making-money.md)).

> Note: You will need to [create an account](https://bantam.io/landing/bundle/@images) in order to test or publish a function.

## Developing Functions - Bantam CLI Walkthrough

Step 1: Download and install the Bantam CLI globally

```
npm install -g @bantam-io/cli
```

Step 2: Configure and login to Bantam

```
bantam configure
```

> This step will prompt you for your `email`, `password`, and your `SECRET KEY`

Step 3: Create a local directory and init a new function

```
cd my-project/
bantam init
```

> This step will prompt you for the `@bundle` and `function name`. Be sure to use a bundle identifier that you own and have created through the dashboard [here](https://bantam.io/develop)

Step 4: Test your function locally

```
cd my-project/@`bundle_identifier`/`function_name`
bantam test
```

Step 5: Publish your function

> Everytime you run bantam publish we overwrite your current function. You also need to make sure to update the version of your function prior to publishing. As you are the owner of the function, it is up to you to manage the versioning.

> `To do this, change the value of "version" in the package.json file.`

```
bantam publish
```

Step 6: Make your function PUBLIC

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
