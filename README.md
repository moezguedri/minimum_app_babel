"# minimum_app_babel"

## Description

This file describes the steps to have a minimal web app setting which includes babel.
It integrates it in VSCode.

## Initialize the project

Create the files 'src/index.js' and 'test.json'.
Run _npm init_; The starting point is src/index.js.

```cmd
npm init
```

## Install npm packages

```cmd
npm install --save-dev babel-cli
npm install --save-dev babel-preset-env
npm install --save-dev babel-watch
```

## Configure 'scripts' in the file package.json

```json
{
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "babel src --out-dir build --source-maps",
    "dev": "npm run build && node build/index.js",
    "watch": "babel src --out-dir build --source-maps --watch"
  }
}
```

Test the configuration:

```cmd
npm run build
```

## Configure VSCode

Under the menu 'Debug' > 'Add configuration...' add a _Node.js_ configuration.
Change the options _program_ and _outFiles_ as follow:

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

You may need to restart VSCode in this stage to take in consideration the changes in launch.json

## Configure Default Build Task

Under the menu _Terminal_ click _Configure Default Build Task_ then chose _npm build_.

You can now execute the compiler by pressing Ctrl+Shift+B.

## Steps to push changes to GitHub:

Commit in VSCode GUI Then run:

```cmd
git push --all
```
