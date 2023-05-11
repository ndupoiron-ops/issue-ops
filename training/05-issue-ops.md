# Issue Ops Use Case

## 1. Disable the wf-create-repo-ops.yml workflow

* Go to your issue-ops repository

* Click on the Actions tab

* Select the `Create Repository on Issue creation via inline scripts` workflow

* Disable workflow on the top-right corner

<img width="365" alt="image" src="https://github.com/ndupoiron-ops/issue-ops/assets/123163496/5e393895-5e6c-4bd5-bdad-2e2d0e4121b4">

The workflow is now disabled

<img width="337" alt="image" src="https://github.com/ndupoiron-ops/issue-ops/assets/123163496/d38c4657-1200-4570-a7eb-236c87c3432d">

## 2. Create a new workflow

* Create a copy of `wf-create-repo-ops.yml` file named `wf-create-repo-ops-action.yml`

* Change workflow name to `Create Repository on Issue creation via actions`

* Replace the first step of the second job with the public action

```yaml
      # Create repository
      - name: Create repository
        id: create_repository
        uses: actions/github-script@v6.3.3
        with:
          github-token: ${{ secrets.REPO_OPS_TOKEN }}
          script: |
            github.rest.repos.createInOrg({
              org: context.repo.owner,
              name: '${{ needs.extract_repository_settings.outputs.repository_name }}',
              visibility: '${{ needs.extract_repository_settings.outputs.repository_visibility }}',
            }).then(({ data }) => {
                core.setOutput("repo_full_name", data.full_name);
                core.setOutput("repo_url", data.html_url);
                core.setOutput("repo_id", data.id);
                core.setOutput("status", "success");
            }
            ).catch((error) => {
                core.setOutput("status", "failure");
                core.setOutput("error", error.response.data.message);
            }
            );
```

replaced by: 

```yaml
      # Create repository
      - name: ndupoiron - Create a repository
        uses: ndupoiron-ops/action-create-repo@v1.0.0
        id: create_repository
        with:
          repo_owner: ${{ github.repository_owner }}
          repo_name: ${{ needs.extract_repository_settings.outputs.repository_name }}
          repo_visibility: ${{ needs.extract_repository_settings.outputs.repository_visibility }}
          token: ${{ secrets.REPO_OPS_TOKEN }}
```

* Create a new issue to test the workflow.

The repository should be created and the issue commented and closed

Now that you know how to use a public action in your workflow, let's have a quick look at the security best practices.

### [Next section: 06 - Security and Policies](https://github.com/tdupoiron-org/issue-ops/blob/main/training/06-policies.md)
