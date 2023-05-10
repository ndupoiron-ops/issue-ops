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
    }
    ).catch((error) => {
        core.setFailed(error.response.data.message);
    }
    );
}

createRepository(repoOwner, repoName, repoVisibility);
```

* Test app using environment variables

```shell
npm install @actions/core

export INPUT_REPO_OWNER=ndupoiron-ops
export INPUT_REPO_NAME=repo03
export INPUT_REPO_VISIBILITY=public
export INPUT_TOKEN=$REPO_OPS_TOKEN

node index.js

::set-output name=repo_full_name::ndupoiron-ops/repo03
::set-output name=repo_url::https://github.com/ndupoiron-ops/repo03
::set-output name=repo_id::638977153
```

 

node index.js 
::error::Repository creation failed.
