## PSTN dial-in for Amazon Chime SDK with Amazon Chime SIP Media Application

[![GitHub stars](https://img.shields.io/github/stars/aws-samples/chime-sipmediaapplication-samples?style=flat-square)](https://github.com/aws-samples/chime-sipmediaapplication-samples/stargazers)
![GitHub contributors](https://img.shields.io/github/contributors/aws-samples/chime-sipmediaapplication-samples?style=flat-square)

Making it easy to add PSTN dialin capabilities to your Amazon Chime SDK Meeting using SIP Media Application

## On this Page
- [Overview](#project-overview)
- [Architecture](#architecture-overview)
- [Setup](#getting-started)
- [Security](#Security)
- [License](#License)

## Overview
Amazon Chime SIP Media Application (SMA) provides PSTN calling support for the Amazon Chime SDK, a feature that enables developers to offer phone numbers and customized interactive voice response (IVR) with their application so that participants can dial-in and dial-out to Chime SDK meetings using a regular telephone. 

## Architecture
![](images/Architecture.svg)

## Setup

### 1. Prerequisites
- [AWS Command Line Interface](https://aws.amazon.com/cli/) in installed
- Repo is cloned
- You have permission to access Amazon Chime Administration Console

### 2. Lambda deployment
Zip you lambda function.
```
zip function.zip index.js
```

Configure AWS Command Line Interface.
```
aws configure
```

Create S3 bucket to upload the lambda code
```
aws s3api create-bucket --bucket source-us-east-1-<accountid> --region us-east-1
```

Package local artifacts
```
aws cloudformation package --template-file ./infrastructre/deployment-template.yaml --s3-bucket source-us-east-1-<accountid> --force-upload --output-template-file packaged.yaml
```

Deploy the lambda
> :warning: **use --parameter-overrides BucketNamePrefixParameter=<string> TableNameParameter=<string> FunctionNameParameter=<string> to overried default values**

```
aws cloudformation deploy --template-file ./packaged.json --stack-name CallAudioDemo --capabilities CAPABILITY_IAM --region us-east-1 
```

### 3. Setup SIP Media Application
- Follow Amazon Chime Admin guide to create SIP Media Application and SIP Rule

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

