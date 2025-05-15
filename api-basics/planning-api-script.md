# Planning an API script

- When you are managing a GitHub repo, you will need to do some tasks like adding and removing people access to the repo

```
https://github.com/dannycuevas/bash-scripts-world/settings/access
```

- You will want some sort of automation for this, and not manually going to the repo "settings" dashboard every time
- To be able to do this, you will need a "shell script" and "GitHub Integration"


## **How does "integration" work**

- On a broad level, **if you want to "talk to any applications", there are 2 ways;**
	- One way is "API"
	- the other way is "CLI"

##### Example with Kubernetes
- When talking to Kubernetes, we use `kubectl` which is a "CLI"
- CLI is a very simple utility
- But for GitHub, the API is much simpler than its CLI


# GitHub API

- We will write our scripts to communicate with the API in any languages;
	- bash
	- python
	- java
- So you can directly talk to the API of GitHub and you can get any required information 

#### GitHub REST API documentation
https://docs.github.com/en/rest?apiVersion=2022-11-28
- This documentation is basically telling us, how can we use the GitHub APIs using the HTTP protocol

- For example, if you want to get a list of pull request of a particular repository, use the following API
	- and below they also share a sample script with the `curl` command
	- and replace the information for ``https://api.github.com/repos/OWNER/REPO/pulls``


#### Tasks of DevOps engineers
These APIs are particularly important because as DevOps engineers, for example, we could implement different tasks using APIs instead of UIs 

- A very common tasks is maintaining repositories 
- You will work with multiple teams, and each team will have their own dedicated repo
- For each repo, you will not only create the repo, but also do tasks like;
	- providing access
	- or removing people from repos 


# Example API call using shell scripting

- Using this shell script we will make an API call that will list all of the users of a github repository 

#### Instructions
- We will need to "export", using the `export` command, our username and token into the terminal in which we will run the script
	- it is done this way so we do not hardcode the values into the script text
```
USERNAME=$username
TOKEN=$token
```

- Also, we will use 2 different arguments when running the script
	- the "repo owner" or the "organization" that is the owner of the repo
	- the "repo name"
```
REPO_OWNER=$1
REPO_NAME=$2
```

### The Script
```
#!/bin/bash

# GitHub API URL
API_URL="https://api.github.com"

# GitHub username and personal access token
USERNAME=$username
TOKEN=$token

# User and Repository information
REPO_OWNER=$1
REPO_NAME=$2

# Function to make a GET request to the GitHub API
function github_api_get {
    local endpoint="$1"
    local url="${API_URL}/${endpoint}"

    # Send a GET request to the GitHub API with authentication
    curl -s -u "${USERNAME}:${TOKEN}" "$url"
}

# Function to list users with read access to the repository
function list_users_with_read_access {
    local endpoint="repos/${REPO_OWNER}/${REPO_NAME}/collaborators"

    # Fetch the list of collaborators on the repository
    collaborators="$(github_api_get "$endpoint" | jq -r '.[] | select(.permissions.pull == true) | .login')"

    # Display the list of collaborators with read access
    if [[ -z "$collaborators" ]]; then
        echo "No users with read access found for ${REPO_OWNER}/${REPO_NAME}."
    else
        echo "Users with read access to ${REPO_OWNER}/${REPO_NAME}:"
        echo "$collaborators"
    fi
}

# Main script

echo "Listing users with read access to ${REPO_OWNER}/${REPO_NAME}..."
list_users_with_read_access
```
