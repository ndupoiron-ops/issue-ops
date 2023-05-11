# Preparation

This chapter is a preparation of the setup required to follow this training.
It simply starts from a free account on GitHub.com.

## 1. Create a new organization

* Sign in to github.com
* Create a new free organization named $username-ops

 <img width="584" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/00003f58-12ba-44a5-8514-188f179d88db">

 The organization name must be unique. 
 This organization will be refered as `dupoiron-org` in the rest of the training
 
 <img width="794" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/54e5cb72-9994-49f9-9992-1dc9a13dd5c4">

## 2. Create a token and secret variables
 
* Navigate to your personal settings

<img width="332" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/439b474c-c697-4478-b13b-9df1580500d3">

* Create a classic Personal Access Token with `admin:org` and `repo` permissions

<img width="527" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/23c7a139-daed-4b13-8763-d286656781d9">

 Save the token as it will be reused in the next step
 
* Navigate to your organization settings and create a secret in both Codespaces and Actions:
 
 <img width="313" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/aaaaa6f3-f1b3-4df7-9eaa-8acb4b84266a">

  - Secret name = REPO_OPS_TOKEN
  - Secret value = < token >

<img width="243" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/ef137496-cba9-4970-93b2-7078ead394b7">

## 3. Test the repo-ops process

* Open the [issue-ops template repository](https://github.com/tdupoiron-org/issue-ops) and click on "Use this template" and create a new public repository
 
<img width="782" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/80c1329d-eba5-4ab6-9889-5e5a07b1943d">

* Open the repository, click on the Actions tab and check that the workflow is enabled
 
<img width="430" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/0705dcaf-d950-4fd5-a6a3-c45ced725667">

* Navigate to `Issues`, and add the `repo-ops` label

<img width="928" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/ba461a89-05cc-498e-8292-f791aab966e2">

* Create a new issue from template. Choose a repository name

<img width="1188" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/75fea32b-aa2c-43d4-9dfa-1d8904f19d19">

The workflow is triggered and the repository should be created.

<img width="401" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/a9b6a9b9-b294-4ce1-a616-88d9a25d4a1d">

At the same time the issue is commented and closed.

<img width="493" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/57fba9ea-b9c9-4be5-acb4-a4adefb9c665">

Your environment is ready, we can move on to section 2.

### [Next section: 02 - Javascript App](https://github.com/tdupoiron-org/issue-ops/blob/main/training/02-javascript-app.md)
