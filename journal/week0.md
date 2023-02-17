# Week 0 — Billing and Architecture
## Week 0 tasks documentation.
This week, I was able to create accounts on gitpod, rollbar, AWS account, honeycomb.io, 



## Installing AWS CLI 
From the AWS-bootcamp-cruddur-2023 template that was forked on github, I used the gitpod button to launch the code editor. I navigated to the `.gitpod.yml` file to update the tasks to be carried out for the installation of the AWS CLI.

I launched the terminal and cd into gitpod/workspace and used these commands:

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install
```
To set the user credentials without using the `aws configure` command, we opened a file with these contents:

```
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION="ca-central-1"
```
Note that I specified the access key and secret access key generated for the user in the admin group that I created on the management console.

To import these values to the AWS CLI, instead of usinng the `aws configure` command on the terminal, we also used the export lines as saved in the file we created above. For example, on the terminal, we used:
```
export AWS_DEFAULT_REGION="ca-central-1"
```

And to confirm if the credentials adding process was successful, I used the command:
```
aws sts get-caller-identity
``` 
This will output the UserId, Account, and ARN of the admin user.

## Getting the credentials to be permanently stored
If we restart the system/process, because we haven't saved t=the user's credentials in gitpod's environment file, the memories about them will be wiped out of the computer. However, to permanently save the credentials that were generated, we have to update the .gitpod.yml file with the following commands:
```
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init:
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT

```
Then on the terminal, we exchanged the word `export` with `gp env` like so:
```
gp env AWS_DEFAULT_REGION="ca-central-1"
```
This is to enable gitpod use it's environment file to save our credentials so that anytime we log into the account, the credentials will always be available for use.


