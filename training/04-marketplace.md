# Marketplace

## 1. Publish release

* Click on Draft a release

<img width="208" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/f7ffaefd-7356-4037-9018-5cbeea662875">

* Verify all requirements

<img width="956" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/8807f141-97b6-401f-ac7e-e2cd0a06869f">

* Create tag v1.0.0 and publish release

<img width="469" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/ce83a0cf-d242-48cf-926c-cd0ad11ff162">

You can find now your action on the Marketplace

<img width="1034" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/e86b0dbb-0500-474f-98df-c36f291ba224">

## 2. Test action from Marketplace

* Create a new workflow file create-repo-test-marketplace.yml in the .github/workflows directory

```yaml
name: Create Repository Test Workflow Marketplace

on:
  workflow_dispatch:
    
    inputs:
      repo_owner:
        description: Owner of the repository to be created
        default: ndupoiron-ops
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
      - name: dupoiron - Create a repository
        uses: dupoiron-ops/action-create-repo@v1.0.0
        with:
          repo_owner: ${{ github.event.inputs.repo_owner }}
          repo_name: ${{ github.event.inputs.repo_name }}
          repo_visibility: ${{ github.event.inputs.repo_visibility }}
          token: ${{ secrets.REPO_OPS_TOKEN }}
```

* Run the workflow manually

The repository should be created as expected

<img width="516" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/9ea0e136-e7e4-49f4-86ab-d429a2782468">

<img width="324" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/4bfef4cf-8a88-4cba-986e-747cd3e8efad">

The action was published to the Marketplace and is now visible for anyone in the public domain. We are going to include it in our initial issue-ops process now.

### [Next section: 05 - Issue Ops process](https://github.com/tdupoiron-org/issue-ops/blob/main/training/05-issue-ops.md)
