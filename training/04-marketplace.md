# Marketplace

## 1. Publish release

* Create tag v1.0.0 and publish release

You can find now your action on the Marketplace

## 2. Test action from Marketplace

* Create a new workflow file create-repo-test-marketplace.yml in the .github/workflows directory

```yaml
name: Create Repository Test Workflow

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
    runs-on: self-hosted

    steps:
      - name: ndupoiron - Create a repository
        uses: ndupoiron-ops/action-create-repo@v1.0.0
        with:
          repo_owner: ${{ github.event.inputs.repo_owner }}
          repo_name: ${{ github.event.inputs.repo_name }}
          repo_visibility: ${{ github.event.inputs.repo_visibility }}
          token: ${{ secrets.REPO_OPS_TOKEN }}
```

* Run the workflow manually

The repository should be created as expected
