# Security and policies

In this section, we will see how to assess actions and create whitelists for developers

## 1. Run security tools on action

* Open action-create-repo repository

* Go to Settings > Code security and analysis

<img width="354" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/7e14ffb9-5015-4005-be6a-3526dab3f0d8">

* Enable Dependabot, Code scanning and Secret scanning

<img width="804" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/b88bc668-a4a5-49da-9857-7b63d24372c1">

<img width="813" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/0db6df08-c1cf-4fd8-b455-7f338589c625">

No vulnerability was found on our project

<img width="302" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/826540eb-eaef-46b6-bce5-bbedb895df1e">

## 2. Create a new release 1.0.1 of the action

<img width="1165" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/3c856cac-8b23-4e6d-b9bd-4cbea3c56173">

## 3. Add action to the whitelist

* Open organization settings

* Go to Actions > General

<img width="315" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/caee9562-ef5b-4802-9097-62e77ceed70c">

* Select "Allow dupoiron-ops actions and reusable workflows"

<img width="960" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/a141fd38-a1ee-422b-acf1-63987c29eb4d">

* Create an issue in the issue-ops repository

GitHub actions are not allowed in project workflows

<img width="679" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/d35a36c7-4e89-4d60-8e62-983ca1778552">

* Change settings and add GitHub created actions and the new one on version 1.0.1

`dupoiron-ops/action-create-repo@v1.0.1`

<img width="965" alt="image" src="https://github.com/tdupoiron-org/issue-ops/assets/7711190/8c114aba-9744-4ac6-bab1-f058739b1669">

* Run the process again, it should work fine now.

Note that it is also possible and even recommended to target an action by its commit sha

```yml
      - name: dupoiron-ops - Create a repository
        uses: dupoiron-ops/action-create-repo@a176e19e880d730a9524123650ceff65cb2c75e4
```

### End

You have reached the end of this training.
Please contact me if you have any question: tdupoiron@github.com
