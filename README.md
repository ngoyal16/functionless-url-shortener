# Functionless URL Shortener
This app creates a URL shortener without using any compute. All business logic is handled at the Amazon API Gateway level. The basic app will create an API Gateway instance utilizing Api Keys for authentication and authorization. It will also create an Amazon DynamoDB table for data storage.


## The Backend

### Services Used
* <a href="https://aws.amazon.com/api-gateway/" target="_blank">Amazon API Gateway</a>
* <a href="https://aws.amazon.com/dynamodb/" target="_bank">Amazon DynamoDB</a>
* <a href="https://aws.amazon.com/cloudfront/" target="_blank">Amazon CloudFront</a> *Will cause a lengthy deployment time. See note under **Deploying**
* <a href="https://aws.amazon.com/s3/" target="_blank">Amazon S3</a>


### Requirements for deployment
* <a href="https://aws.amazon.com/cli/" target="_blank">AWS CLI</a>
* <a href="https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html" target="_blank">AWS SAM CLI v0.37.0+</a>

### Deploying

***Note: This stack includes an Amazon CloudFront distribution which can take around 30 minutes to create. Don't be alarmed if the deploy seems to hang for a long time.***
In the terminal, use the SAM CLI guided deployment the first time you deploy
```bash
sam deploy -g
```

```shell
sam deploy -g --config-file samconfig.toml --config-env prd
```

#### Choose options
You can choose the default for all options except *GithubRepository* and **

```bash
## The name of the CloudFormation stack
Stack Name [URLShortener]:

## The region you want to deploy in
AWS Region [ap-south-1]:

## The name of the application (lowercase no spaces). This must be globally unique
Parameter AppName [shortener]:

## AWS OrgId to protect APIs using IAM Auth to only account related to AWS Orgs 
Parameter OrgId []:

## Domain Name for the shortener.
Parameter CustomDomainName []:

## Shows you resources changes to be deployed and requires a 'Y' to initiate deploy
Confirm changes before deploy [y/N]: 

## SAM needs permission to be able to create roles to connect to the resources in your template
Allow SAM CLI IAM role creation [Y/n]:

## Save your choice for later deployments
Save arguments to samconfig.toml [Y/n]:
```

SAM will then deploy the AWS CloudFormation stack to your AWS account and provide required outputs for the included client.

After the first deploy you may re-deploy using `sam deploy` or redeploy with different options using `sam deploy -g`.

## Cleanup
1. Open the <a href="https://ap-south-1.console.aws.amazon.com/cloudformation/home" target="_blank">CloudFormation console</a>
1. Locate a stack named *URLShortener*
1. Select the radio option next to it
1. Select **Delete**
1. Select **Delete stack** to confirm

*Note: If you opted to have access logs (on by default), you may have to delete the S3 bucket manually.
