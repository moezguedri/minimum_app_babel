"# minimum_app_babel"

## Description

This file describes the steps to have a minimal web app setting which includes babel.
It integrates it with VSCode.

## Initialize

The starting point is src\index.js

```cmd
npm init
```

## Install npm packages

```cmd
npm install --save-dev babel-cli babel-preset-env babel-watch
npm install --save graphql apollo-server
npm install --save-dev babel-plugin-graphql-tag babel-plugin-import-graphql
```

## Create the files src\index.js and src\query.graphql

## Configure the scripts in the file package.json

```json
{
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "babel src --out-dir build --source-maps",
    "debug": "npm run build && node build/index.js",
    "build_and_watch": "babel src --out-dir build --source-maps --watch"
  }
}
```

Test the configuration:
npm run build

## Configure VSCode

Under the menu Debug > Add configuration... add a Node.js configuration.
Change the options 'program' and 'outFiles' as follow:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "program": "${workspaceFolder}/src/index.js",
      "outFiles": ["${workspaceRoot}/build/**/*.js"]
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Current File",
      "program": "${file}",
      "outFiles": ["${workspaceRoot}/build/**/*.js"]
    },
    {
      "type": "node",
      "request": "attach",
      "name": "Attach",
      "processId": "${command:PickProcess}"
    }
  ]
}
```

You may need restart VSCode in this stage to take in consideration the changes in launch.json

## Configure Default Build Task

Under the menu Terminal click 'Configure Default Build Task' then chose 'npm build'.
You can now execute the TypeScript compiler by pressing Ctrl+Shift+B.
