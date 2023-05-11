# issue-ops

## Introduction
In the previous training we learned the basics of GitHub Actions by creating simple workflows. 

We also covered how to create reusable workflows.

A reusable workflow starts independent runners where steps are executed.

This is useful to orchestrate a series of actions and offer these reusable processes to developers.

But it is not sufficient to design an easy to understand and performant process if we only deal with reusable workflows and inline scripts.

This is why it is preferrable to combine them with actions. A custom action can be created from a Javascript app or a Docker image.

The documentation is [here](https://docs.github.com/en/actions/creating-actions/about-custom-actions)

## Use Case
The objective is to build a IssueOps process to allow developers to create repositories from requests hosted in issues.

This allows the DevSecOps teams to keep control on repository creation and policies enforcement.

## Start the training

Follow the guide starting with [Section 1 - Preparation](https://github.com/tdupoiron-org/issue-ops/blob/main/training/01-preparation.md)
