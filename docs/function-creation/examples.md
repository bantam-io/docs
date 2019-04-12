# Examples

By providing some simple configurations, you can add a "Try it Out!" tab to the Bantam function dashboard page for users to test your function.

In order to generate these examples, all you need to do is add an `examples` array underneath a `bantam` key in the `package.json` file.

When the function is published next, the "Try it Out!" tab will be activated. [See here](https://bantam.io/functions/@images/metadata) an example of the "Try it Out!" tab.

Example:

```javascript
inside package.json...

  "bantam": {
    "examples": [
      {
        "name": "Image Resize",
        "description": "Resize the image down to 500px width.",
        "type": "image",
        "arguments": {
          "url": "https://images.pexels.com/photos/1637108/pexels-photo-1637108.jpeg",
          "width": 500
        }
      },
      {
        "name": "Image Contain / Low Quality",
        "description": "Resize the image to be contained within a 500x200px image. Also, reduce the quality of the image.",
        "type": "image",
        "arguments": {
          "url": "https://images.pexels.com/photos/1637108/pexels-photo-1637108.jpeg",
          "width": 500,
          "height": 200,
          "method": "inside",
          "quality": 80
        }
      },
      {
        "name": "Black & White",
        "description": "Make the image black and white, and resize the image down to 500px width.",
        "type": "image",
        "arguments": {
          "url": "https://images.pexels.com/photos/1637108/pexels-photo-1637108.jpeg",
          "width": 500,
          "filter": "greyscale"
        }
      }
    ]
  },

  ...
```

Publishing the function with the above examples would result in a dropdown on the "Try it Out!" page with three different prefilled examples: "Image Resize", "Image Contain / Low Quality", and "Black and White".

## Example Arguments

Each object inside of the examples array has the following arguments:

- **name** - _(required, string)_ - This is the name of the example. It will appear in the example dropdown on the dashboard.
- **description** - _(optional, string)_ - A short description that will be displayed underneath the example title.
- **type** - _(optional, default=`json`, string)_ - This will determine if the response will be displayed as JSON or an image. If your function is related to returning/modifying images, you will likely want to set this to `image`:
  - `JSON`: The response will be in JSON format.
  - `image`: The response will render the returned image.
- **method** - _(optional, string)_ - If your function has multiple methods, this will preset the example to call that method. If left blank, the default method will be invoked.
- **arguments** - _(default = {}, object)_ - This object containers all of the arguments used within the function handler you wrote. It will be the default set of arguments placed in the code editor within the page.
