> This page contains a brief setup description for CI/CD pipelines in GitHub Actions workflows. `dev` branch uses that.

> **CONTENT**

- [Build workflows YAML definitions](#build-workflows-yaml-definitions)
  - [GitHub Actions Build workflows](#github-actions-build-workflows)
- [On Pull Request Builds](#on-pull-request-builds)
- [On Push Builds](#on-push-builds)
- [GitHub Composite Actions](#github-composite-actions)
- [Additional References](#additional-references)

## Build workflows YAML definitions

Folder `/.github/workflows/` has all the YAML files for all build workflows. Although (for simplicity reasons) `eShopOnContainers` that has all code in the same repo, we have one separated build per microservice. All builds have two jobs (named `BuildContainersForPR_Linux` and `BuildLinux`) that build the Linux version of the microservice for each PR and push on the `dev` branch.

We use _path filters_ to queue only the build when commits have files in certain paths. For example, this is the _path filters_ sections of the Web Status microservice:

```yaml
  paths:
    - src/BuildingBlocks/**
    - src/Web/WebStatus/**
    - .github/workflows/webstatus.yml
```

The build will be triggered if the commits have some file in these folders. Any other change won't trigger the build. Using _path filters_ we have the flexibility to use a single repository, separated builds, and trigger only the needed builds.

Please, refer the [GitHub Actions](https://docs.github.com/en/actions) for more information.

### GitHub Actions Build workflows

We have a build workflow for each service in GitHub Actions created from the YAML file. To create the `build` workflow from an existing YAML file, create a new build workflow in GitHub Actions:

![Create a new workflow - step1](./images/GitHub-Actions/create-new-workflow.png)

After choosing a new workflow, either you can define your workflow YAML from scratch or choose the Feature Actions from the Market place.
To define the workflow file, you can leverage the online YAML editor.

![Create a new workflow - step2](./images/GitHub-Actions/configure-new-workflow.png)

## On Pull Request Builds

We have enabled the build workflows for `pull_request` event on `dev` branch.For that each workflow has `BuildContainersForPR_Linux` job. There are some differences between a normal build and the build triggered by a PR though:

The build triggered from a PR do not push the docker images to any docker registry.

![Build On PR](./images/GitHub-Actions/github-actions-build-pr.png)

## On Push Builds

We have enabled the build workflows for `push` event on `dev` branch.
For that each workflow has `BuildLinux` job. Each push event builds the docker image and push it to the dockerhub.

![Build On PUSH](./images/GitHub-Actions/github-actions-build-push.png)

## GitHub Composite Actions

Recently, all the GitHub workflows have been refactored with the help of [GitHub Composite Actions](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action). You can find the PR and discussions in [here](https://github.com/dotnet-architecture/eShopOnContainers/pull/1753). 

If you want to know more about it, please refer to [GitHub Composite Actions](https://colinsalmcorner.com/github-composite-actions/)

## Additional References

- [eShopOnContainers docker image scanning with GitHub Actions](
https://faun.pub/eshoponcontainers-experiment-with-image-scanning-21b73ac5c4b7)

