# github-to-lambda-demo

This is a demo project used to configure a simple cicd to AWS Lambda.

# Project Architecture
GitHub  --(push)--> Build in AWS CodeBuild linking via GitHub actions --(update)--> AWS Lambda 

# Steps To Create Demo
## GitHub
- Create a repository in Github
- Create a [personal Token](https://github.com/settings/tokens) [(any help)](https://stackoverflow.com/questions/68775869/message-support-for-password-authentication-was-removed-please-use-a-personal), for later on authentication purposes
- Add the files: lambda_function.py, requirements.txt, and buildspec.yml to the repo

## In AWS
- 
