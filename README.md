Overview
========

This project is here to help you with deployement of NodeJS application to [AWS Lambda](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) using [Bitbucket Pipelines](https://confluence.atlassian.com/bitbucket/build-test-and-deploy-with-pipelines-792496469.html).
For Deployement [Claudia](https://claudiajs.com/tutorials/installing.html) tool is used.

Usage
=====
0. Copy source files (bitbucket-pipelines.yml, pre-deploy) in project directory.
1. Configure Claudia for your NodeJS project [docs](https://claudiajs.com/tutorials/installing.html)
2. Paste deployement command to ```package.json``` inside ```scripts``` section in root directory of your your project.
Example:
```json
{
  ...
  "scripts": {
    "deploy": "TMPDIR=/tmp claudia update --version master --use-s3-bucket apiMaster --set-env LOCAL_DEV=false --timeout 30 --profile claudia",
  }
  ...
```

Note the ```TMPDIR=/tmp```. It's a woraround for [known bug](https://github.com/ysugimoto/aws-lambda-image/issues/125) so make sure you do not miss it in your configuration.

3. Configure AWS IAM keys (if you did not do it on step 1).
4. Set up environment variables ```AWS_ACCESS_KEY_ID``` and ```AWS_SECRET_ACCESS_KEY``` (AWS IAM access key id and AWS IAM access key respectively) in for Bitbucket repository [docs](https://confluence.atlassian.com/bitbucket/environment-variables-794502608.html)
5. Modify bitbucket-pipelines.yml if needed.