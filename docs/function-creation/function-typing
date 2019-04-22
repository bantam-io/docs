# Function Typing

Function typing allows us to make Bantam function integrate with IDEs as if it's native code. You can provide the expected inputs and outputs, and we'll handle the rest.

- [Simple Example](#example)
- [Usage](#Usage)

## Example

Before documenting, let's take a look at an example, let's consider the function [@simple/log]([https://bantam.io/functions/@simple/log](https://bantam.io/functions/@simple/log)).

We have a few methods (`@simple/log` `@simple/log/warn`, `@simple/log/error`, and `@simple/log/critical`), so there are a few good examples.

Inside our functions `package.json` file, we can put our typings like this:

```json
"bantam": {
      {
        "title": "Info Log",
        "description": "A simple logger with level `info`. You can pass in a `message`, `info`, or both",
        "args": {
          "message": {
            "description": "A text value to go along with the log.",
            "dataType": "string"
          },
          "info": {
            "description": "Any data of the log",
            "dataType": "any"
          }
        }
      },
      {
        "title": "Warning Log",
        "description": "A simple logger with level `warn`. You can pass in a `message`, `info`, or both",
        "method": "warn",
        "args": {
          "message": {
            "description": "A text value to go along with the log.",
            "dataType": "string"
          },
          "info": {
            "description": "Any data of the log",
            "dataType": "any"
          }
        }
      },
      {
        "title": "Error Log",
        "description": "A simple logger with level `error`. You can pass in a `message`, `info`, or both",
        "method": "error",
        "args": {
          "message": {
            "description": "A text value to go along with the log.",
            "dataType": "string"
          },
          "info": {
            "description": "Any data of the log",
            "dataType": "any"
          }
        }
      },
      {
        "title": "Critical Log",
        "description": "A simple logger with level `critical`. You can pass in a `message`, `info`, or both",
        "method": "critical",
        "args": {
          "message": {
            "description": "A text value to go along with the log.",
            "dataType": "string"
          },
          "info": {
            "description": "Any data of the log",
            "dataType": "any"
          }
        }
      }
```

## Usage

Underneath the `bantam` object in the function's package.json, you can provide the value `typings`. Each value outlines one set of method/input/output.

Each type is structured like this:

- `title` - *required* - The title of this use-case
- `description` - *required* - A description of this use case
- `method` - *optional* - If this is using a method to your function (reminder: format is `@bundle/function/method`, then provide it here.
- `args`- *required* - This is an object outlining the input arguments. For each argument, you the value has this structure:
  - `description`: A description for this value.
  - `dataType`: One of the following options:
    - `"number"`
    - `"string"`
    - `"boolean"`
    - `"null"`
    - `"any"`
    - An object to futher nest arguments. The value of the object has the same structure as the `args` object, so it infinitely nests.
  - `required`: *optional* - Only if you want it required, provide the boolean `true`
