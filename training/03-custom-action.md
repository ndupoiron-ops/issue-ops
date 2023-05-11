# Custom Action

## 1. Use GitHub core

* Edit script to replace the inputs/outputs with the core object

```javascript
const core = require('@actions/core');
const { Octokit } = require("@octokit/rest");

// Get Input Parameters
const repoOwner = core.getInput('repo_owner');
const repoName = core.getInput('repo_name');
const repoVisibility = core.getInput('repo_visibility');
const token = core.getInput('token')

const octokit = new Octokit({
  auth: token,
});

async function createRepository(repoOwner, repoName, repoVisibility) {

    octokit.rest.repos.createInOrg({
        org: repoOwner,
        name: repoName,
        visibility: repoVisibility
    }).then(({ data }) => {
        core.setOutput("repo_full_name", data.full_name);
        core.setOutput("repo_url", data.html_url);
        core.setOutput("repo_id", data.id);
        core.setOutput("status", "success");
    }
    ).catch((error) => {
        core.setFailed(error.response.data.message);
        core.setOutput("status", "failure");
    }
    );
}

createRepository(repoOwner, repoName, repoVisibility);
```

* Test app using environment variables

```shell
npm install @actions/core

export INPUT_REPO_OWNER=dupoiron-ops
export INPUT_REPO_NAME=repo03
export INPUT_REPO_VISIBILITY=public
export INPUT_TOKEN=$REPO_OPS_TOKEN

node index.js

::set-output name=repo_full_name::dupoiron-ops/repo03
::set-output name=repo_url::https://github.com/dupoiron-ops/repo03
::set-output name=repo_id::639087573
::set-output name=status::success
```

* Run job again to see what happens when the creation fails

```shell
node index.js 
::error::Repository creation failed.
::set-output name=status::failure
```

* Build app using webpack

```shell
npm run build
```

## 2. Creation Action definition

* Creation an `action.yml` file at the root directory

```yaml
name: 'dupoiron - Create a repository'
description: 'Create a repository'

branding:
  icon: 'arrow-right-circle'
  color: 'green'

inputs:

  repo_owner:
    description: The name of the repository
    required: true

  repo_name:
    description: The name of the repository
    required: true

  repo_visibility:
    description: The visibility of the repository
    required: false
    default: public

  token:
    description: The access token used to authenticate to the GitHub API
    required: true

outputs:
  repo_id:
    description: The ID of the repository
  repo_full_name:
    description: The full name of the repository
  repo_url:
    description: The URL of the repository

runs:
  using: "node16"
  main: "dist/action.js"
```  

* Push the code to the main branch

You can see that it is now possible to publish the action to the marketplace

<img width="920" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/f6ecafaf-b965-49c1-a11d-44056ad88c2f">

## 3. Test the local action in a simple workflow

* Go to Action tab

* Search for manual workflow and configure it
 
 <img width="315" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/e43aaf82-49e8-41be-b680-ccff2aa70b3f">

* Rename the file `create-repo-test-local.yml` and paste the following content

```yaml
name: Create Repository Test Workflow Local

on:
  workflow_dispatch:
    
    inputs:
      repo_owner:
        description: Owner of the repository to be created
        default: dupoiron-ops
        type: string
      
      repo_name:
        description: Name of the repository to create
        type: string
        required: true
        
      repo_visibility:
        description: can be public or private
        type: string
        default: public

jobs:
  create_repo:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v3.5.2

    - name: Create a repository
      uses: ./
      with:
        repo_owner: ${{ github.event.inputs.repo_owner }}
        repo_name: ${{ github.event.inputs.repo_name }}
        repo_visibility: ${{ github.event.inputs.repo_visibility }}
        token: ${{ secrets.REPO_OPS_TOKEN }}

```

* Commit and push to main

* Go to the Actions tab and run the workflow manually

<img width="344" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/5ad73284-c947-482c-9f25-b897dfc7bc6c">

The workflow has run and invoked the local action thanks to the following attribute: `uses: ./`

A repository is created as indicated

Now that our action is ready, we can publish it to the Marketplace

### [Next section: 04 - Marketplace](https://github.com/tdupoiron-org/issue-ops/blob/main/training/04-marketplace.md)
