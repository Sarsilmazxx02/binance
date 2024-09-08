# Binance connector in Nodejs in Editing JSON with Visual Studio Code

[![npm version](https://badge.fury.io/js/%40binance%2Fconnector.svg)](https://badge.fury.io/js/%40binance%2Fconnector)
[![Node version](https://img.shields.io/node/v/%40binance%2Fconnector.svg?style=flat)](http://nodejs.org/download/)
[![Standard-Js](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[README (2).md](https://github.com/user-attachments/files/16923716/README.2.md)
[coinstats_template.csv](https://github.com/user-attachments/files/16923717/coinstats_template.csv)
[b5d0ad84d0f46651fb380b1cc5eb23600a2482dd963866564e353f7113d6c2db_en_usd.pdf](https://github.com/user-attachments/files/16924018/b5d0ad84d0f46651fb380b1cc5eb23600a2482dd963866564e353f7113d6c2db_en_usd.pdf)
[bitcoin.pdf](https://github.com/user-attachments/files/16924013/bitcoin.pdf)
[README (2).md](https://github.com/user-attachments/files/16924012/README.2.md)

# Visual Studio Code
Version 1.93 is now available! Read about the new features and fixes from August.

Dismiss this update
Topics 

# JSON
Editing JSON with Visual Studio Code
JSON is a data format that is common in configuration files like package.json or project.json. We also use it extensively in Visual Studio Code for our configuration files. When opening a file that ends with .json, VS Code provides features to make it simpler to write or modify the file's content.

# JSON within VS Code

IntelliSense and validation
For properties and values, both for JSON data with or without a schema, we offer up suggestions as you type with IntelliSense. You can also manually see suggestions with the Trigger Suggestions command (Ctrl+Space).

We also perform structural and value verification based on an associated JSON schema giving you red squiggles. To disable validation, use the json.validate.enable setting.

IntelliSense

Package and project dependencies
We also offer IntelliSense for specific value sets such as package and project dependencies in package.json, project.json, and bower.json.

Quick navigation
JSON files can get large and we support quick navigation to properties using the Go to Symbol command (Ctrl+Shift+O).

# Goto Symbol

Hovers
When you hover over properties and values for JSON data with or without schema, we will provide additional context.

Hover

Formatting
You can format your JSON document using Ctrl+Shift+I or Format Document from the context menu.

Folding
You can fold regions of source code using the folding icons on the gutter between line numbers and line start. Folding regions are available for all object and array elements.

# JSON with Comments
In addition to the default JSON mode following the JSON specification, VS Code also has a JSON with Comments (jsonc) mode. This mode is used for the VS Code configuration files such as settings.json, tasks.json, or launch.json. When in the JSON with Comments mode, you can use single line (//) as well as block comments (/* */) as used in JavaScript. The mode also accepts trailing commas, but they are discouraged and the editor will display a warning.

The current editor mode is indicated in the editor's Status Bar. Select the mode indicator to change the mode and to configure how file extensions are associated to modes. You can also directly modify the files.associations setting to associate file names or file name patterns to jsonc.

JSON schemas and settings
To understand the structure of JSON files, we use JSON schemas. JSON schemas describe the shape of the JSON file, as well as value sets, default values, and descriptions. The JSON support shipped with VS Code supports all draft versions from draft 4 to draft 7, with limited support for drafts 2019-09 and 2020-12.

Servers like JSON Schema Store provide schemas for most of the common JSON-based configuration files. However, schemas can also be defined in a file in the VS Code workspace, as well as the VS Code settings files.

The association of a JSON file to a schema can be done either in the JSON file itself using the $schema attribute, or in the User or Workspace settings (File > Preferences > Settings) under the property json.schemas.

VS Code extensions can also define schemas and schema mapping. That's why VS Code already knows about the schema of some well-known JSON files such as package.json, bower.json, and tsconfig.json.

Mapping in the JSON
In the following example, the JSON file specifies that its contents follow the CoffeeLint schema.

{
  "$schema": "https://json.schemastore.org/coffeelint",
  "line_endings": "unix"
}
Copy
Note that this syntax is VS Code-specific and not part of the JSON Schema specification. Adding the $schema key changes the JSON itself, which systems consuming the JSON might not expect, for example, schema validation might fail. If this is the case, you can use one of the other mapping methods.

Mapping in the User Settings
The following excerpt from User Settings shows how .babelrc files are mapped to the babelrc schema located on https://json.schemastore.org/babelrc.

"json.schemas": [
    {
        "fileMatch": [
            "/.babelrc"
        ],
        "url": "https://json.schemastore.org/babelrc"
    }
]
Copy
Tip: In addition to defining a schema for .babelrc, also make sure that .babelrc is associated to the JSON language mode. This is also done in the settings using the files.association array setting.

Mapping to a schema in the workspace
To map a schema that is located in the workspace, use a relative path. In this example, a file in the workspace root called myschema.json will be used as the schema for all files ending with .foo.json.

```json
.schemas": [
    {
        "fileMatch": [
            "**/*.foo.json"
        ],
        "url": "./myschema.json"
    }
]

Mapping to a schema defined in settings
To map a schema that is defined in the User or Workspace settings, use the schema property. In this example, a schema is defined that will be used for all files named .myconfig.

```


```json.schemas": [
    {
        "fileMatch": [
            "/.myconfig"
        ],
        "schema": {
            "type": "object",
            "properties": {
                "name" : {
                    "type": "string",
                    "description": "The name of the entry"
                }
            }
        }
    }
]

```

# Mapping a schema in an extension
Schemas and schema associations can also be defined by an extension. Check out the jsonValidation contribution point.


```File match syntax
The file match syntax supports the '*' wildcard. Also, you can define exclusion patterns, starting with '!'. For an association to match, at least one pattern needs to match and the last matching pattern must not be an exclusion pattern.

  "json.schemas": [
    {
      "fileMatch": [
        "/receipts/*.json",
        "!/receipts/*.excluded.json"
      ],
      "url": "./receipts.schema.json"
    }
  ]

```


```
Define snippets in JSON schemas
JSON schemas describe the shape of the JSON file, as well as value sets and default values, which are used by the JSON language support to provide completion proposals. If you are a schema author and want to provide even more customized completion proposals, you can also specify snippets in the schema.

The following example shows a schema for a key binding settings file defining a snippet:

{
    "type": "array",
    "title": "Keybindings configuration",
    "items": {
        "type": "object",
        "required": ["key"],
        "defaultSnippets": [
            {
                "label": "New keybinding",
                "description": "Binds a key to a command for a given state",
                "body": { "key": "$1", "command": "$2", "when": "$3" }
            }
        ],
        "properties": {
            "key": {
                "type": "string"
            }
            ...
        }
    }
}

```
## This is an example in a JSON schema:

Default snippets in JSON schema

Use the property defaultSnippets to specify any number of snippets for the given JSON object.

label and description will be shown in the completion selection dialog. If no label is provided, a stringified object representation of the snippet will be shown as label instead.
body is the JSON object that is stringified and inserted when the completion is selected by the user. Snippet syntax can be used inside strings literals to define tabstops, placeholders, and variables. If a string starts with ^, the string content will be inserted as-is, not stringified. You can use this to specify snippets for numbers and booleans.
Note that defaultSnippets is not part of the JSON schema specification but a VS Code-specific schema extension.

Use rich formatting in hovers
VS Code will use the standard description field from the JSON Schema specification in order to provide information about properties on hover and during autocomplete.

```
If you want your descriptions to support formatting like links, you can opt in by using Markdown in your formatting with the markdownDescription property.

{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "name": {
      "type": "string",
      "description": "The name of the entry",
      "markdownDescription": "The name of the entry. [See the documentation](https://example.com)"
    }
  }
}

 ```
## Note that markdownDescription is not part of the JSON schema specification but a VS Code-specific schema extension.

Offline mode
json.schemaDownload.enable controls whether the JSON extension fetches JSON schemas from http and https.

A warning triangle will show in the status bar when the current editor would like to use schemas that cannot be downloaded.








This is a lightweight library that works as a connector to [Binance public API](https://github.com/binance/binance-spot-api-docs). It’s designed to be simple, clean, and easy to use with minimal dependencies.

- Supported APIs:
    - `/api/*`
    - `/sapi/*`
    - Spot Websocket Market Stream
    - Spot User Data Stream
    - Spot Websocket API
- Inclusion of test cases and examples
- Customizable base URL
- Support request timeout and HTTP proxy (since v2)
- Response metadata can be displayed
- Customizable Logger


## Installation

```bash
npm install @binance/connector
```

## Documentation

[https://binance.github.io/binance-connector-node/](https://binance.github.io/binance-connector-node/)

## RESTful APIs

```javascript
const { Spot } = require('@binance/connector')

const apiKey = 'c9f3tCe0l34EUaaPSiL9s0KtyRC4mDG0rK4KRPTdxiqhjrCrbgZeTibcexLLApP0'
const apiSecret = 'Cittld17y7ynFYzy7NeexmVy0uzLV23OOS1JHFKfz95X1aLFP7Vv75gmCSqmGqL5'
const client = new Spot(apiKey, apiSecret)

// Get account information
client.account().then(response => client.logger.log(response.data))

// Place a new order
client.newOrder('BNBUSDT', 'BUY', 'LIMIT', {
  price: '350',
  quantity: 1,
  timeInForce: 'GTC'
}).then(response => client.logger.log(response.data))
  .catch(error => client.logger.error(error))
```

Please find `examples` folder to check for more endpoints.

## Key Pair Based Authentication

```javascript
const { Spot, PrivateKeyAlgo } = require('@binance/connector')

const apiKey = 'c9f3tCe0l34EUaaPSiL9s0KtyRC4mDG0rK4KRPTdxiqhjrCrbgZeTibcexLLApP0'
const apiSecret = ' Cittld17y7ynFYzy7NeexmVy0uzLV23OOS1JHFKfz95X1aLFP7Vv75gmCSqmGqL5 ' // has no effect when RSA private key is provided

// load private key
const privateKey = fs.readFileSync('/Users/john/ssl/private_key_encrypted.pem')
const privateKeyPassphrase = 'password'
const privateKeyAlgo = PrivateKeyAlgo.RSA // for RSA key
const privateKeyAlgo = PrivateKeyAlgo.ED25519 // for Ed25519 key

const client = new Spot(apiKey, apiSecret, {
  privateKey,
  privateKeyPassphrase, // only used for encrypted key
  privateKeyAlgo
})

// Get account information
client.account().then(response => client.logger.log(response.data))
```

### Testnet

While `/sapi/*` endpoints don't have testnet environment yet, `/api/*` endpoints can be tested in
[Spot Testnet](https://testnet.binance.vision/). You can use it by changing the base URL:

```javascript
// provide the testnet base url
const client = new Spot(apiKey, apiSecret, { baseURL: 'https://testnet.binance.vision'})
```

### Base URL

If `base_url` is not provided, it defaults to `api.binance.com`.

It's recommended to pass in the `base_url` parameter, even in production as Binance provides alternative URLs in case of performance issues:

- `https://api1.binance.com`
- `https://api2.binance.com`
- `https://api3.binance.com`

### Optional Parameters

Optional parameters are encapsulated to a single object as the last function parameter.

```javascript
const { Spot } = require('@binance/connector')

const apiKey = 'c9f3tCe0l34EUaaPSiL9s0KtyRC4mDG0rK4KRPTdxiqhjrCrbgZeTibcexLLApP0'
const apiSecret = 'Cittld17y7ynFYzy7NeexmVy0uzLV23OOS1JHFKfz95X1aLFP7Vv75gmCSqmGqL5'
const client = new Spot(apiKey, apiSecret)

client.account({ recvWindow: 2000 }).then(response => client.logger.log(response.data))

```

### Timeout

It's easy to set timeout in milliseconds in request. If the request take longer than timeout, the request will be aborted. If it's not set, there will be no timeout.

```javascript
const { Spot } = require('@binance/connector')

const apiKey = 'c9f3tCe0l34EUaaPSiL9s0KtyRC4mDG0rK4KRPTdxiqhjrCrbgZeTibcexLLApP0'
const apiSecret = 'Cittld17y7ynFYzy7NeexmVy0uzLV23OOS1JHFKfz95X1aLFP7Vv75gmCSqmGqL5'
const client = new Spot(apiKey, apiSecret, { timeout: 1000 })

client.account()
  .then(response => client.logger.log(response.data))
  ios` package is used as the http client in this library. A proxy settings is passed into `axios` directly, the details can be found at [here](https://github.com/axios/axios#request-config):

```javascript
const { Spot } = require('@binance/connector')

const apiKey = 'c9f3tCe0l34EUaaPSiL9s0KtyRC4mDG0rK4KRPTdxiqhjrCrbgZeTibcexLLApP0'
const apiSecret = 'Cittld17y7ynFYzy7NeexmVy0uzLV23OOS1JHFKfz95X1aLFP7Vv75gmCSqmGqL5'
const client = new Spot(apiKey, apiSecret,
  {
    proxy: {
      protocol: 'https',
      host: '127.0.0.1',
      port: 9000,
      auth: {
        username: 'proxy_user',
        password: 'password'
      }
    }
  }
)
```

You may have a HTTP proxy, that can bring the problem that you need to make a HTTPS connection through the HTTP proxy.  You can do that by build a HTTPS-over-HTTP tunnel by npm package [tunnel](https://www.npmjs.com/package/tunnel), and then pass the turnnel agent to `httpsAgent` in `axios`.

```javascript
const tunnel = require('tunnel')

const agent = tunnel.httpsOverHttp({
  proxy: {
    host: "127.0.0.1",
    port: 3128
  }
})

const client = new Spot(null, null,
  {
    baseURL: "https://api.binance.com",
    httpsAgent: agent
  }
)

client.time()
  .then(response => client.logger.log(response.data))
  

```
[This comment](https://github.com/axios/axios/issues/925#issuecomment-359982190) provides more details.

### Response Metadata

The Binance API server provides weight usages in the headers of each response. This information can be fetched from `headers` property. `x-mbx-used-weight` and `x-mbx-used-weight-1m` show the total weight consumed within 1 minute.

```
// client initialization is skipped

client.exchangeInfo().then(response => client.logger.log(response.headers['x-mbx-used-weight-1m']))

```

### Custom Logger Integration

```javascript
const Spot = require('@binance/connector')
const fs = require('fs')
const { Console } = require('console')

// make sure the logs/ folder is created beforehand
const output = fs.createWriteStream('./logs/stdout.log')
const errorOutput = fs.createWriteStream('./logs/stderr.log')

const logger = new Console({ stdout: output, stderr: errorOutput })
const client = new Spot('', '', {logger: logger})

client.exchangeInfo().then(response => client.logger.log(response.data))
// check the output file

```

The default logger defined in the package is [Node.js Console class](https://nodejs.org/api/console.html). Its output is sent to `process.stdout` and `process.stderr`, same as the global console.



## Websocket

#  "json.schemas": [
    {
        "fileMatch": [
            "**/*.foo.json"
        ],
        "url": "./myschema.json"
    }
]



"json.schemas": [
    {
        "fileMatch": [
            "/.myconfig"
        ],
        "schema": {
            "type": "object",
            "properties": {
                "name" : {
                    "type": "string",
                    "description": "The name of the entry"
                }
            }
        }
    }
]

  "json.schemas": [
    {
      "fileMatch": [
        "/receipts/*.json",
        "!/receipts/*.excluded.json"
      ],
      "url": "./receipts.schema.json"
    }
  ]

 ```
### Websocket Stream
```javascript
const { WebsocketStream } = require('@binance/connector')
const logger = new Console({ stdout: process.stdout, stderr: process.stderr })

// define callbacks for different events
const callbacks = {
  open: () => logger.debug('Connected with Websocket server'),
  close: () => logger.debug('Disconnected with Websocket server'),
  message: data => logger.info(data)
}

const websocketStreamClient = new WebsocketStream({ logger, callbacks })
// subscribe ticker stream
websocketStreamClient.ticker('bnbusdt')
// close websocket stream
setTimeout(() => websocketStreamClient.disconnect(), 6000)

```

### Unsubscribe Websocket Stream

```javascript
// unsubscribe websocket stream
websocketStreamClient.unsubscribe('bnbusdt@kline_1m')
```

### WebSocket API

```javascript
const { WebsocketAPI } = require('@binance/connector')
const logger = new Console({ stdout: process.stdout, stderr: process.stderr })

// callbacks for different events
const callbacks = {
  open: (client) => {
    logger.debug('Connected with Websocket server')
    // send message to get orderbook info after connection open
    client.orderbook('BTCUSDT')
    client.orderbook('BNBUSDT', { limit: 10 })
  },
  close: () => logger.debug('Disconnected with Websocket server'),
  message: data => logger.info(data)
}

const websocketAPIClient = new WebsocketAPI(null, null, { logger, callbacks })

// disconnect the connection
setTimeout(() => websocketAPIClient.disconnect(), 20000)

```

More websocket examples are available in the `examples` folder


### Auto Reconnect

If there is a close event not initiated by the user, the reconnection mechanism will be triggered in 5 secs.

### Ping Server

It is possible to ping server from client, and expect to receive a PONG message.

```javascript
websocketStreamClient.pingServer()
```

### Custom Logger Integration

The default logger defined in the package is [Node.js Console class](https://nodejs.org/api/console.html). Its output is sent to `process.stdout` and `process.stderr`, same as the global console.

Note that when the connection is initialized, the console outputs a list of callbacks in the form of `listen to event: <event_name>`.

## Test

```bash
 {
  "$schema": "https://json.schemastore.org/coffeelint",
  "line_endings": "unix"
}
  npm install

"json.schemas": [
    {
        "fileMatch": [
            "/.babelrc"
        ],
        "url": "https://json.schemastore.org/babelrc"
    }
]

```

## Limitation

Futures and Vanilla Options APIs are not supported:

  - 
[Binance api key.txt](https://github.com/user-attachments/files/16923714/Binance.api.key.txt)
`/fapi/*`
  - `/dapi/*`
  - `/vapi/*`
  -  Associated Websocket Market and User Data Streams

## License
MIT
