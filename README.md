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

i. on events
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

i. uses
- identifier an action to use
- defines the location of that action

ii. run
- runs commands in the virtual environment's shell

iii. name
- an optional identifier for the step