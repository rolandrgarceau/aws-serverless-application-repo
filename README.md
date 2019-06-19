# AWS Serverless Application Repo now available at AWS GovCloud (us-west) Region

20190611 AWS released the repo in aws govclound us-west region. We can use this as a means
to publish or consume publicly available applications. Models for creating apps use
AWS SAM, and may not be limited to CloudFormation templates, but is one of AWS services
with means to auto-deploy resources. This directory will explore scaffolding a 
few consumable projects and see how we may map a set of definitions when 
building our own projects for the cloud. 

This repo is designed as a step to "don't reinvent the wheel if you can" approach 
for my rov-project prior to commencing code writing, and is a good architectural 
approach in general to address already built or common open sourced concerns 
when developing solutions.

## Table of Contents
### How to follow this repo
Files can be read by friendly-descriptive-names that correspond to topics below.
You may read them with my suggested 00- based numbering prefix, or jump right to 
specifics, the numbering is just a guide that may assist injesting some heavier 
topics here.

*Exploring The Repository:
    capabilities-and-dep-mgmt
        You have to acknowledge permissions and policies first prior to deploying
    nested-applications
        May be an abstraction of containerization and need to be realized prior too.
*Serverless Application Model (SAM) 
    api-gateway-and-sam
        RESTful ways (or otherwise) to interact with serverless apps from AWS
    sam-cli-commands
        AWS SAM cli for interacting with resources via a terminal or script. 
*CloudFormation
    Templating with YAML or other included spec like, xml parsable, ./configure settings.
*Lambda
    AWS service with "lambda" functions that assist management of serverless apps.

*Amazon Container Services
*Docker
*Kubernetes

## Gotchas
When dealing with downloading prebuilt templates we have to perform some investigation
of their configuration files and map out the resources required to replicate the project.
Out the gate we know we will have to deal with it operating in AWS account resources,
so we have to define all the IAM permissions fow AWS, then look at the other services 
needed within the account and could potentially have some rather tricky policy 
building preformed, especially if resources are external to AWS- like say, Google
Firebase.io that will require your google credentials, and then possibly an 
authorization flow that is incorporated with OAuth2 or others that require accounts
external to AWS. 

We also may hsve to deal with CORS, and API Gateway, and Lambda- all of which 
require sufficient knowledge and configuration in their own right to bring into 
a working, replicated application flow. Relax, we will chew it one byte at a time. 
Some more complex configurations get abstracted away daily, like authorization 
flows for API integrations. The Table of Contents will be updated as we dissect 
more of the repository. 

## Additional Resources and links to documentation

Release of the repo news with links to docs:
https://aws.amazon.com/about-aws/whats-new/2019/06/serverless-application-repository-available-in-govcloud-region-us-west/?sc_channel=em&sc_campaign=GLOBAL_LA_NL_Engaged-Newsletter_20190618&sc_medium=em_166290&sc_content=PA_nl_la&sc_geo=mult&sc_country=global&sc_outcome=pa&trk=em_166290&mkt_tok=eyJpIjoiWTJFd05EVTVNV0k1T1RkbCIsInQiOiJnTjErRDJoT2h4TmJYOVVRUDhtNytcL041TVVabmZHcnc0Z1lEUXBlZ0R4UXAyUjNZeW5pakNVNUxYM1c4YTNRejJHSURRRFhWR0thUGpZdFwvcjJiRGJJMGNDUUV4TVZZejhpVkd2MENpTHFnazdmZDJmZlpEXC9PbEZWT3BTMG5oSjRyR1lTaGZcL1BUN0x6U1A5RDRmRHpBPT0ifQ%3D%3D

The SAM guide:
https://aws.amazon.com/serverless/sam/

API Gateway within SAM for authorization:
https://aws.amazon.com/about-aws/whats-new/2018/10/aws-sam-supports-amazon-api-gateway-authorizers/

OAuth is another avenue to be versed on:
https://oauth.net/2/

Firebase is from Google:
https://firebase.google.com/?gclid=EAIaIQobChMI_eqe4oL04gIV1gOGCh2YewjDEAAYASAAEgKil_D_BwE

