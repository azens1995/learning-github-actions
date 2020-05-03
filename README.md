# Github Actions
## Build Status Badge: ![](https://github.com/azens1995/learning-github-actions/workflows/first/badge.svg)

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

---

## checkout action:
checks out all the repository code into te  computer environments file system making files available to the 
steps that runs in the job

---

## run
execute commands in the operating system's default shell
    * bash: Default shell for Ubuntu, macOS
    * powershell: Default shell for Windows

| Run | Syntax |
| --- | ---    |
| Single-line command | <p>run: {command} {parameters} {arguments}</br>run: mv ./output ./archive</p> |
| Multiple command    | <p>run: &#124;</br>Command 1</br>Command 2</br>run: &#124;</br>g++ -c -Wall -g Main.cpp<br>g++ -g -o Main.exe Main.io</p> |

-----

## Trigerring workflows manually using the repository dispatch event

```
name: Manually trigger workflow using repository dispatch
on:
    repository_dispatch
        types: [build]
    jobs:
        trigger-manual-workflow:
            runs-on: ubuntu-latest
            steps:
                - name: Payload from manual trigger
                  run: echo ${{ github.event.client_payload.env }}
```

Github workflow can be manually triggered by making the API call to the url provided by the github.
Requirements:
```
1. URL: https://api.github.com/repos/azens1995/learning-github-actions/dispatch
     https://api.github.com/repos/{username}/{repository}/dispatch

2. Request Type: POST
3. Headers:
 1. Accept: application/vnd.github.dorian-preview+json
 2. Content-Type: application/json

4. Body [raw, json]
    {
	"event_type": "build",
	"client_payload": {
		"env": "production"
	}
}

5. Authorization
    Type: Basic Auth
    Username: leave-this-empty
    Password: token-generated-from-github
```

### Generating the Token from the Github
We can generate the token from the github to use for making of the post request.
Profile 
    > Settings 
        > Developer Settings 
            > Personal Access Tokens 
                > Generate New Token
                    > Note: Add the note for the token
                    > Check the `repo` and generate the token

### Event_Type
    The event type used in the post request should be the same in the yaml file too.
    As we have seen here the use of the `build` in the post request as well as in the yaml file under the `repostiry_dispatch`'s type to be `build`.

    That is the first step to connect the custom trigger dispatch.
    The second thing is we can add the payload to the post request too. To add the payload: </br>
    ```
    {
        "event_type": "NAME",
        "client_payload": {
            "KEY": "VALUE"
        }
    }
    ```

    Now, we can access this payload in the YAML file using the github access as: </br>
    ```
        run: echo ${{ github.event.client_payload.KEY }}
    ```

