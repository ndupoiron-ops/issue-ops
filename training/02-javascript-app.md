# Javascript application

## 1. Initialize project

* Create the `action-create-repo` public repository in the organization

* Start a Codespace on this repository

You can see that the secret is available in the codespace

* Open a terminal and initialize a new nodeJS project:

```shell
npm init

package name: (boostrap) repo-ops
version: (1.0.0) 
description: Create repository from issue
```

* Add a .gitignore

```
node_modules
```

## 2. Design a script to create a repository

* Create a index.js file with the following code

```javascript
const { Octokit } = require("@octokit/rest");

// Get Input Parameters
const repoOwner = process.env.REPO_OWNER
const repoName = process.env.REPO_NAME
const repoVisibility = process.env.REPO_VISIBILITY
const token = process.env.REPO_OPS_TOKEN

const octokit = new Octokit({
    auth: token
  });
  
async function createRepository(repoOwner, repoName, repoVisibility) {

    octokit.rest.repos.createInOrg({
        org: repoOwner,
        name: repoName,
        visibility: repoVisibility
    }).then(({ data }) => {
        console.log("repo_full_name", data.full_name)
        console.log("repo_url", data.html_url);
        console.log("repo_id", data.id);
    }
    ).catch((error) => {
        console.log(error.response.data.message);
    }
    );
}

createRepository(repoOwner, repoName, repoVisibility);
```

* Install dependencies and test script

```shell
npm install @octokit/rest
export REPO_OWNER=ndupoiron-ops
export REPO_NAME=repo01
export REPO_VISIBILITY=private

node index.js

repo_full_name ndupoiron-ops/repo01
repo_url https://github.com/ndupoiron-ops/repo01
repo_id 638974808
```

A repository `repo01` is created in your organization

## 3. Build app using webpack

* Install webpack

```shell
npm install --save-dev webpack
npm install --save-dev webpack-cli
npm install node-polyfill-webpack-plugin
```

*	Create webpack.config.js configuration file

```javascript
const path = require('path');
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin")

module.exports = {

  target: 'node',

  mode: "production",
  entry: './index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'action.js',
  },

  optimization: {
    minimize: true
  },
  
};
```

* Change package.json to add build command

```json
  "scripts": {
    "build": "webpack --config webpack.config.js"
  },
```

* Run build

```shell
npm run build

> repo-ops@1.0.0 build
> webpack --config webpack.config.js

asset action.js 415 KiB [emitted] [minimized] (name: main) 1 related asset
orphan modules 188 KiB [orphan] 31 modules
runtime modules 937 bytes 4 modules
javascript modules 323 KiB
  modules by path ./ 323 KiB
    cacheable modules 134 KiB
      modules by path ./node_modules/@actions/ 65.9 KiB 10 modules
      modules by path ./node_modules/whatwg-url/lib/*.js 41.8 KiB 5 modules
      modules by path ./node_modules/before-after-hook/ 3.68 KiB 4 modules
      modules by path ./node_modules/tunnel/ 7.49 KiB 2 modules
      + 5 modules
    ./node_modules/@octokit/rest/dist-web/index.js + 16 modules 179 KiB [not cacheable] [built] [code generated]
    ./node_modules/uuid/dist/esm-node/index.js + 15 modules 9.86 KiB [not cacheable] [built] [code generated]
  + 11 modules
./node_modules/tr46/lib/mappingTable.json 254 KiB [built] [code generated]
webpack 5.82.0 compiled successfully in 3371 ms
```

action.js is created and minimized in dist folder.

* Test package

```shell
export INPUT_REPO_OWNER=ndupoiron-ops
export INPUT_REPO_NAME=repo02
export INPUT_REPO_VISIBILITY=public

node dist/action.js

repo_full_name ndupoiron-ops/repo02
repo_url https://github.com/ndupoiron-ops/repo02
repo_id 638980724
