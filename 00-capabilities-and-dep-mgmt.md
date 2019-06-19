To begin using projects from the repo, we need to outline the changes within the 
deployment files. These get checked prior to deploy. You have to acknowledge the
"capabilities" prior to using them, as they may escalate privelages on your account.
Then you may initiate a deployment into an Amazon account. Be aware that if we see the 
AWS::Serverless::Application resource, it may mean there is a nested application
that needs additional acknowledgement for prior to using the original app in question.
Make sure you read the nested-applications notes file on this, or visit the docs.

Nested Applications
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-template-nested-applications.html

Acknowledgement of capabilities:
https://docs.aws.amazon.com/serverlessrepo/latest/devguide/acknowledging-application-capabilities.html

to review via AWS cli:
aws serverlessrepo get-application \
--application-id application-arn 

For info on the Application applicationId
https://docs.aws.amazon.com/serverlessrepo/latest/devguide/applications-applicationid.html#applications-applicationid-prop-version-requiredcapabilities

Values that must be specified in order to deploy some applications:
CAPABILITY_IAM
CAPABILITY_NAMED_IAM
CAPABILITY_AUTO_EXPAND
CAPABILITY_RESOURCE_POLICY

Also be aware that when using an app from the repo you may also affect resources
in the account that include but not be limited to:

IAM roles: AWS::IAM::Group, AWS::IAM::InstanceProfile, AWS::IAM::Policy, and AWS::IAM::Role.

Resource policies: AWS::Lambda::LayerVersionPermission, AWS::Lambda::Permission, AWS::Events::EventBusPolicy, AWS::IAM:Policy, AWS::ApplicationAutoScaling::ScalingPolicy, AWS::S3::BucketPolicy, AWS::SQS::QueuePolicy, and AWS::SNS:TopicPolicy.

You may use a SDK per language to get the application, but we will stick with 
javascript and python as it is the two that fuel Lambda functions needed for 
serverless applications in AWS.

Javascript
https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/ServerlessApplicationRepository.html#getApplication-property

Python


We really want to dissect projects available from the repo to ascertain what AWS
includes in a deployment. So we need to know what files provide configuration,
and each may be by individual project. On a high level, generally there may be:

A CloudFormation template

May also contain configuration for container management
Amazon Containers

Kubernetes

Docker 

We will explore these more on a per project basis.