# Pricing

## Setting Price with your Bantam Config File (package.json)

After getting logged in, creating a bundle, and getting the Bantam CLI installed, then running `bantam init`. Your function's package.json file will allow you to set the memory, timeout, and pricing of your function.

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
    "public": true,
    "publicPrice": 0.523
  },
  "author": "me",
  "license": "ISC",
  "private": true,
  "dependencies": {}
}
```

To determine what your `publicPrice` should be, you first must pick one of the below combinations of memory and timeout to find the max charge you will incure before your function times-out.

`{ "memory": { "timeout": price } }`

#### Bantam pricing structure:

Memory &nbsp; / &nbsp; Timeout &nbsp; / &nbsp; Price

```
128   /   5     /  0.0000108688
128   /   30    /  0.00006421280000000002
128   /   300   /  0.000640328
128   /   900   /  0.001920584

256   /   5     /  0.000021537600000000002
256   /   30    /  0.00012822560000000003
256   /   300   /  0.001280456
256   /   900   /  0.003840968

512   /   5     /  0.0000428752
512   /   30    /  0.00025625120000000005
512   /   300   /  0.002560712
512   /   900   /  0.007681736

1024   /   5     /  0.00008555040000000001
1024   /   30    /  0.0005123024000000001
1024   /   300   /  0.005121224
1024   /   900   /  0.015363272

2048   /   5     /  0.0001709008
2048   /   30    /  0.0010244048
2048   /   300   /  0.010242248
2048   /   900   /  0.030726344

3008   /   5     /  0.0002509168
3008   /   30    /  0.0015045008
3008   /   300   /  0.015043208
3008   /   900   /  0.045129224
```

If you were to choose from the pricing structure above, a memory of `128`, and a timeout of `30` seconds, you would then do a lookup on the pricing structure, to find the minimum `publicPrice` you could set your function to charge would be `0.00006421280000000002`.

Then, depending on the `publicPrice` your choose, your `bantam` config object would then look something like:

```
"bantam": {
    "memory": 128,
    "timeout": 30,
    "public": true,
    "publicPrice": 0.05
  },
```

Once your have finalized your function, running `bantam publish` would submit your new pricing structure.
