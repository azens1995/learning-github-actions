# Github Actions

## Workflows and Actions Attributes

```
name: Hello World
on: [push]
jobs:
    say-hello:
        runs-on: ubuntu-latest
        steps:
            -name: checkout
            uses: actions/checkout@v2.0.0
            -run: echo Hello World
```
1. name
- The name of the workflow
- not required

2. on
- The github event that triggers the workflow
- required

    1. on events
        - Repository events
        - Push
        - pull_request
        - release
        - web hooks
            -- branch creation
            -- issues
            -- members
        - scheduled
            -- cron format

3. jobs
- workflows must have at least one job
- each job must have an identifier
- must start with a letter or underscore
- can only contain alphanumeric character, -, or _

4. runs-on
- the type of the machin to run the job
- runners
    -- windows server 2019
    -- unbuntu
    -- macOS

5. steps
- list of actions or commands
- access to the file system
- each step runs in its own process

    1. uses
        - identifier an action to use
        - defines the location of that action

    2. run
        - runs commands in the virtual environment's shell

    3. name
        - an optional identifier for the step

---
## Adding an Action
* uses: execute an action in operating system

| Action Location | Syntax |
| --- | --- |
| Public Repository | <p>uses: {owner}/{repo}/@{ref}<br>uses: octocat/super-cool-action@v1</p> |
| The same repository as the workflow | <p>uses: ./path/to/the/action<br>uses: ./.github/actions/my-cool-action</p> |
| A docker image registry | <p>uses: docker://{image}:{tag}<br>uses: docker://hello-world:latest</p> |