---
title: Publishing Hugo with GitHub Actions
date: 2024-09-25T17:13:35.495Z
lastmod: 2024-09-25T17:13:35.495Z
draft: false
description: test Deploying Hugo remotely with Github Actions.
summary: test Deploying Hugo remotely with Github Actions.
tags:
    - Github Actions
    - Deployment
    - SSH
categories:
    - Reference
authors: haifeng
isCJKLanguage: false
slug: publishing-hugo-github-actions
---

## What are GitHub Actions?

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your software development workflows directly in your GitHub repository. It enables you to build, test, and deploy your code from GitHub.Some key points about GitHub Actions:

- It allows you to create workflows that are triggered by various GitHub events like push, pull request, issues, etc. [](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions)[](https://dev.to/akebu6/github-actions-explained-bne)
- Workflows are defined using YAML syntax in the .github/workflows directory in your repository [](https://codefresh.io/learn/github-actions/github-actions-workflows-basics-examples-and-a-quick-tutorial/)
- Each workflow consists of one or more jobs which run in parallel or sequentially [](https://codefresh.io/learn/github-actions/github-actions-workflows-basics-examples-and-a-quick-tutorial/)
- Jobs are made up of steps which can run commands or use actions provided by the community [](https://codefresh.io/learn/github-actions/github-actions-workflows-basics-examples-and-a-quick-tutorial/)
- GitHub provides Linux, Windows, and macOS virtual machines to run your workflows, or you can use self-hosted runners [](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions)
- It supports a wide range of programming languages and frameworks [](https://assets.ctfassets.net/wfutmusr1t3h/6IyfnYAidl3QUoX2xfGOgI/6aa9e5df02378f952f7c1ba5f42effc9/What-is-GitHub.Actions_.Benefits-and-examples.pdf)
- GitHub Actions is included in GitHub Free, GitHub Pro, and GitHub Enterprise plans with varying usage limits [](https://assets.ctfassets.net/wfutmusr1t3h/6IyfnYAidl3QUoX2xfGOgI/6aa9e5df02378f952f7c1ba5f42effc9/What-is-GitHub.Actions_.Benefits-and-examples.pdf)

GitHub Actions goes beyond just CI/CD and enables automating any part of your development workflow. Some popular use cases include [](https://assets.ctfassets.net/wfutmusr1t3h/6IyfnYAidl3QUoX2xfGOgI/6aa9e5df02378f952f7c1ba5f42effc9/What-is-GitHub.Actions_.Benefits-and-examples.pdf):

- Automating repetitive tasks like issue triage and pull request reviews
- Running code linters, formatters, and tests on every commit
- Building, testing, and packaging applications for deployment
- Deploying to cloud services like Azure, AWS, or Google Cloud
- Interacting with external services via webhooks

In summary, GitHub Actions provides a powerful and flexible platform to automate your software development lifecycle directly within GitHub.

## Build a Publish GitHub Workflow

Like some of the other GitHub features, e.g., PR and issue templates, workflows reside in the `.github` of a repository in the subfolder `workflows`. The actual filename doesn’t have much relevance, but let’s call it `publishHugo.yml`.

### The Basic Structure

Here’s the basic structure of GitHub Action workflow file:

```yaml

name: Publish Hugo

on: push

jobs:
  deploy:

    runs-on: ubuntu-22.04

    steps:
      - ...

```

The keys are quite self-explanatory, but let’s go over them:

`name:`
The name of your workflow

`on:`
One or more events that trigger your workflow. You’re not limited to Git events, though, as workflows can also run on events like “issue created” and others. For this blog, however, only push is required. You can check out all the possible events in the [documentation](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows).

`jobs:`
One or more jobs that will run in Docker containers. In the example. A job has a series of steps that are either a pre-defined action, or you can run commands and shell scripts directly in the container.

### Defining Job Steps

To design the pipeline requires you to establish the required steps first. Remember, GitHub Actions start from a simple Docker container with a base image, so you need to set up the environment, too:

- Checkout the repository
- Deploy to remote server
- Build Hugo

As GitHub Action can run arbitrary commands and scripts, you could create a shell script doing all these things and just run it.

### GitHub Actions

In essence, GitHub Actions are tasks written running in Node.js with access to a lot of GitHub features. Actions allow a workflow to concentrate _what it’s supposed to do_ and not _how to do it_.

#### Check the repository

[`actions/checkout@v4`](https://github.com/actions/checkout)

```yaml
- uses: actions/checkout@v4
    with:
        submodules: true  # Fetch Hugo themes (true OR recursive)
        fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod
```

Let’s go over the different keys:
`uses:`
Which action the step uses.
`with:`
Anything under this key is action-specific configuration. In my case, Congo theme is added with Hugo Module method，so submodules should be fetched as well.

#### Deploy to Remote Server

Publishing Hugo in a remote server would require GitHub to `SSH` to server firstly and run cmds like `git pull` and `hugo --minify` remotely.

The [`appleboy/ssh-action@v1.0.3`](https://github.com/appleboy/ssh-action) action simplifies those into a single step:

```yaml
- name: Deploy to Remote Server
    uses: appleboy/ssh-action@v1.0.3
    with:
        host: ${{ secrets.REMOTE_HOST }}
        username: ${{ secrets.REMOTE_USER }}
        key: ${{ secrets.REMOTE_PRIVATE_KEY }}
        script: |
            cd /path/to/your/website
            git pull origin main
            hugo --minify
            sudo systemctl restart nginx
```

The ssh-action requires `REMOTE_HOST` `REMOTE_USER` and `REMOTE_PRIVATE_KEY` are required for remote server SSH.

Looking back at the broadly defined steps from the previous section, these GitHub Actions emerge:
