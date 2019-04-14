# Pricing

Price per call is set in the package.json file.  

<br/>

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

To determine what your minimum `publicPrice` should be, choose a combinations of memory and timeout to find the max charge you will incure before your function times-out. NOTE: If your function calls other Bantam functions (for example `@simple/file-download`), you should include those fees in your price.

<br/>

## Bantam pricing structure:

Memory &nbsp; / &nbsp; Timeout &nbsp; / &nbsp; Price

```
128    /   5     /  0.00006067
128    /   30    /  0.00011401

256    /   5     /  0.00007134
256    /   30    /  0.00017803

512    /   5     /  0.00009268
512    /   30    /  0.00030605

1024   /   5     /  0.00013535
1024   /   30    /  0.0005621

2048   /   5     /  0.0002207
2048   /   30    /  0.0010742

3008   /   5     /  0.00030072
3008   /   30    /  0.0015543
```

The minimum allowed `publicPrice` is the Bantam price per call.  For example, if your function needs `128` megabytes of memory with a `30` second timeout, then the `publicPrice` must be at least `0.00011401`.

Then, depending on the `publicPrice` you choose, your `bantam` config object would then look something like:

```
"bantam": {
    "memory": 128,
    "timeout": 30,
    "publicPrice": 0.05
  },
```

Once your have finalized your function, running `bantam publish` will submit your new pricing structure.

Keep in mind when publishing a config with the bantam config object `{ "bantam": { public: false } }`, your function will <b>not</b> be public to Bantam users. To make your function `PUBLIC`,set `public` to `true` before running `bantam publish`. For more information about public and private functions, check out our [docs here](../function-creation/public-functions.md)

#### Updating price

To protect you and your users.  Once a function is used by outside users, you cannot raise the `publicPrice` by more than 50% in a 30 day timespan. Therefore make sure you select a reasonable starting price.
