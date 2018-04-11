# aws-batch-cfn-with-ci-cd
POC to showcase Batch with CodePipeline

This POC requires the NetworkStackName parameter which is referring  to the stack created by the VPC template in the [Startup Kit Templates](https://github.com/aws-samples/startup-kit-templates).


The following is an example script to launch this template. You must define the parameters at the top.

```
#!/bin/bash

VPC_STACK_NAME=CHANGE_ME
GITHUB_TOKEN=CHANGE_ME
GITHUB_USER=CHANGE_ME
GITHUB_REPO=CHANGE_ME
GITHUB_BRANCH=CHANGE_ME

aws cloudformation create-stack --stack-name test-batch-1 --template-body file://batch.cfn.yml \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters \
    ParameterKey=NetworkStackName,ParameterValue=$VPC_STACK_NAME \
    ParameterKey=GitHubSourceRepo,ParameterValue=$GITHUB_REPO \
    ParameterKey=GitHubUser,ParameterValue=$GITHUB_USER \
    ParameterKey=GitHubBranch,ParameterValue=$GITHUB_BRANCH \
    ParameterKey=GitHubToken,ParameterValue=$GITHUB_TOKEN
```

The [aws-batch-sample-job-python](https://github.com/rnzsgh/aws-batch-sample-job-python) repo provides an example job complete with
the [buildspec.yml](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html) and
a [Job Definition Template](https://docs.aws.amazon.com/batch/latest/userguide/job-definition-template.html) example.
