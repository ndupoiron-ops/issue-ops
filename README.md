# issue-ops

## Introduction
In the previous training we learned the basics of GitHub Actions by creating simple workflows. We also have seen how to create reusable workflows.
A reusable workflow starts independent runners where steps are executed.
This is useful to orchestrate a series of actions and offer these reusable processes to developers.

But it is not easy to design and test complex processes in workflows inline scripts.
This is why it might be preferrable to create a custom action. A custom action can be created from a Javascript app or a Docker image.

The documentation is here: https://docs.github.com/en/actions/creating-actions/about-custom-actions
Use Case
The objective is to build a IssueOps process to let developers create repositories from requests hosted in issues. This allows the DevSecOps teams to keep control on repository creation and policies enforcement.
