This chapter is a preparation of the tools required to follow this training.
It simply requires a free account on GitHub.com.

# 1 - Create a new organization

* Sign in to github.com
* Create a new free organization
* Give it a name <username>-ops
 
 The organization name must be unique. 
 This organization will be refered as ndupoiron-org in the rest of the training
 
* Create a new repository named "action-create-repo"

# 2 - Create a token and secret variables
 
* Navigate to your personal settings and create a classic Personal Access Token with admin:org and repo permissions

 Save the token as it will be reused in the next step
 
* Navigate to your organization settings and create a secret in Codespaces and Actions:
 
 Secret name = REPO_OPS_TOKEN
 Secret value = <token>

# 3 - Test the repo-ops process

* Open https://github.com/ndupoiron-ops/issue-ops and click on "Use this template" and create a new repository
 
* Open the repository, click on the Actions tab and enable the workflows
 
 <img width="481" alt="image" src="https://github.com/ndupoiron-ops/issue-ops/assets/123163496/4cafc352-cb66-409a-bf9c-0f7d1d0b1a87">

* Create a new issue from template. Choose a repository name

 Don't forget to create the repo-ops label
 
 <img width="346" alt="image" src="https://github.com/ndupoiron-ops/issue-ops/assets/123163496/af63f298-7bdd-4e37-baf6-221bdea78dfe">

The workflow is triggered and the repository should be created. 
At the same time the issue is commented and closed.
