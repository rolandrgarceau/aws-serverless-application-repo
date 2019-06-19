Be aware that if we see the AWS::Serverless::Application resource, it may mean 
there is a nested application that needs additional acknowledgement for, and 
prior to using or deploying the original app in question from the repo.

Nested Applications documentation
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-template-nested-applications.html

Nested applications may be what some know as a compiled containerized binaries 
that may be included in the packaging as a layered component, or defined as a 
dependency within the appropriate configuration file, which may need to draw 
from source and compile on the fly, per the called out inclusion within the 
project, at deploy time- or just simply included in a config. 

Nested apps have currently an included max at 200 per project (check for 
changes when you do a pull), for the severless application repo. The nested apps 
also only allow up to 60 parameters. docs didn't say each, but was implied- test 
it if you are getting close for a use case.

Nested apps may be part of the public repo, part of your private app list within 
your AWS account, or even on your local machine, so beware of builds that require
them, the locations where they may be gound, and what lengths you may need to go 
to scaffold together them for that particular project.

These commonly nested programs may be deemed as dedicated applications within an 
existing application template and may be solidified as time goes on within the 
Model itself- if it is a piece that is found regularly in the repo. We need to 
explore more to see patterns here. For now lets just focus on the SAM, its repo 
and the capabilities called out for replication. If you want more info on 
containerization of applications by layer, or "one offs" and how they may be 
built into a dockerfile, see my repo on rov-testing under docker.