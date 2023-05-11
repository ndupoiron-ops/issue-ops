# Javascript application

In this chapter we will create a simple Javascript app to invoke GitHub Javascript SDK to create a repository.

## 1. Initialize project

* Create the `action-create-repo` public repository in the same organization and inititalize it with the default README file.

<img width="537" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/e22f1510-ae8d-4363-8d1a-98db8f654c6f">

* Start a Codespace on this repository

<img width="424" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/1444f3dd-c0d4-4804-b008-6edec827f3ee">

You can see that the secret is available in the codespace

```shell
echo $REPO_OPS_TOKEN
```

* Open a terminal and initialize a new nodeJS project:

```shell
npm init

package name: (action-create-repo) 
version: (1.0.0) 
description: Create repository from issue
```

* Add a `.gitignore` file

```
node_modules
```

<img width="300" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/1e0d0746-5748-4089-bb74-d3cc1b0711fc">

## 2. Design a script to create a repository

* Create an `index.js` file with the following code

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
export REPO_OWNER=dupoiron-ops
export REPO_NAME=repo01
export REPO_VISIBILITY=private

node index.js

repo_full_name dupoiron-ops/repo01
repo_url https://github.com/dupoiron-ops/repo01
repo_id 639064493
```

A repository `repo01` is created in your organization

<img width="343" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/17a6cceb-d07c-4fd4-9b60-8b0cff1fb41d">

## 3. Build app using webpack

* Install webpack

```shell
npm install --save-dev webpack
npm install --save-dev webpack-cli
npm install node-polyfill-webpack-plugin
```

*	Create `webpack.config.js` configuration file

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

> action-create-repo@1.0.0 build
> webpack --config webpack.config.js

asset action.js 382 KiB [emitted] [minimized] (name: main) 1 related asset
orphan modules 179 KiB [orphan] 18 modules
runtime modules 937 bytes 4 modules
built modules 493 KiB [built]
  cacheable modules 314 KiB
    modules by path ./node_modules/whatwg-url/lib/*.js 41.8 KiB 5 modules
    modules by path ./node_modules/before-after-hook/ 3.68 KiB
      ./node_modules/before-after-hook/index.js 1.71 KiB [built] [code generated]
      + 3 modules
    modules by path ./node_modules/tr46/ 261 KiB
      ./node_modules/tr46/index.js 7.39 KiB [built] [code generated]
      ./node_modules/tr46/lib/mappingTable.json 254 KiB [built] [code generated]
    + 4 modules
  ./node_modules/@octokit/rest/dist-web/index.js + 18 modules 179 KiB [not cacheable] [built] [code generated]
  external "punycode" 42 bytes [built] [code generated]
webpack 5.82.1 compiled successfully in 2584 ms
```

action.js is created and minimized in dist folder.

* Test package

```shell
export REPO_OWNER=dupoiron-ops
export REPO_NAME=repo02
export REPO_VISIBILITY=public

node dist/action.js

repo_full_name dupoiron-ops/repo02
repo_url https://github.com/dupoiron-ops/repo02
repo_id 639065654
```

Once again, the repository is created successfully

<img width="328" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/8d2d5257-88ed-4bb6-9f5b-cda769f2e12f">

You have successfully created and tested a Javascript app to operate the creation of a repository. We can now translate this app into an Action.

### [Next section: 03 - Custom action](https://github.com/tdupoiron-org/issue-ops/blob/main/training/03-custom-action.md)
