# github-to-lambda-demo

This is a demo project used to configure a simple cicd to AWS Lambda.

# Project Architecture
GitHub  --(push)--> Build in AWS CodeBuild linking via GitHub actions --(update)--> AWS Lambda 

# Steps To Create Demo
## In AWS Lambda
- Create a empty Python Lambda function 

## GitHub
- Create a repository in Github
- Create a [personal Token](https://github.com/settings/tokens) [(any help)](https://stackoverflow.com/questions/68775869/message-support-for-password-authentication-was-removed-please-use-a-personal), for later on authentication purposes
- Add the files: lambda_function.py, requirements.txt, and buildspec.yml to the repo
  - requirements.txt file contains project dependencies
  - lambda_function.py contains the Lambda code
  - buildspec.yml contains the build steps, which will be executed by CodeBuild

## In AWS CodeBuild
- Create a CodeBuild Project
- Link the project with GitHub project. [Create a build project with GitHub](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-github-pull-request.html) 
- For the attached CodeBuild's IAM role add the following permissions inorder to update the respective Lambda:
- (Path to the IAM role: CodeBuild Project &#8594; Build details &#8594; Environemnt &#8594; Service role)
```json
{
    "Effect": "Allow",
    "Action": [
        "lambda:AddPermission",
        "lambda:RemovePermission",
        "lambda:CreateAlias",
        "lambda:UpdateAlias",
        "lambda:DeleteAlias",
        "lambda:UpdateFunctionCode",
        "lambda:UpdateFunctionConfiguration",
        "lambda:PutFunctionConcurrency",
        "lambda:DeleteFunctionConcurrency",
        "lambda:PublishVersion"
    ],
    "Resource": "arn:aws:lambda:us-east-1:your-aws-account-number:function:your-lambda-function-name"
}
```

## Testing
- Commit and push the changes to the main branch of the GitHub repo, AWS CodeBuild would be triggred and the linked Lambda function will be updated by 
