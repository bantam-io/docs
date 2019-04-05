# Pricing

## Setting Price with your Bantam Config File (package.json)

After getting logged in, creating a bundle, getting the Bantam CLI installed, and running `bantam init`, your function's package.json file will allow you to set the memory, timeout, and pricing of your function.

<br/>
#### Example function package.json:

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
    "public": false,
    "publicPrice": 0.05
  },
  "author": "me",
  "license": "ISC",
  "private": true,
  "dependencies": {}
}
```

To determine what your `publicPrice` should be, you first must pick one of the below combinations of memory and timeout to find the max charge you will incure before your function times-out.

<br/>
#### Bantam pricing structure:

Memory &nbsp; / &nbsp; Timeout &nbsp; / &nbsp; Price

```
128   /   5     /  0.0000108688
128   /   30    /  0.00006421280000000002

256   /   5     /  0.000021537600000000002
256   /   30    /  0.00012822560000000003

512   /   5     /  0.0000428752
512   /   30    /  0.00025625120000000005

1024   /   5     /  0.00008555040000000001
1024   /   30    /  0.0005123024000000001

2048   /   5     /  0.0001709008
2048   /   30    /  0.0010244048

3008   /   5     /  0.0002509168
3008   /   30    /  0.0015045008
```

If you were to choose from the pricing structure above, a memory of `128`, and a timeout of `30` seconds, you would then do a lookup on the pricing structure, to find the minimum `publicPrice` you could set your function to charge would be `0.00006421280000000002`.

Then, depending on the `publicPrice` your choose, your `bantam` config object would then look something like:

```
"bantam": {
    "memory": 128,
    "timeout": 30,
    "public": false,
    "publicPrice": 0.05
  },
```

Once your have finalized your function, running `bantam publish` would submit your new pricing structure.

Keep in mind when submitting a config with the bantam config object `{ "bantam": { public: true } }`, your function will be live and public to all Bantam users. To keep your function private for testing, just make sure to set that false before going live. For more information about how public vs private functions, check out our [docs here](../function-creation/public-functions.md)
