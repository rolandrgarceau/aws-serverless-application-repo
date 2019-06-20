# Testing workflow solutions between a local machine environment and AWS  
This repo can be used as a tool when looking through AWS Serverless Application 
repository and developing testing workflows for deployment of their pre-built
solutions. Manual version management per language and service may be an alternative 
to this suggested approach, and can be mixed and matched for individual use cases.

## Prerequisites
A firm grasp of Linux, Node.js, Python, CI/CD pipelines on AWS, and Docker. 

## The problem
Containerizing serverless node.js applications for AWS to test locally on your
machine is not as easy as deploying that same application with Lambda to your AWS
account. SAM cli can be used to package and run your Lambda function locally, but
testing and debugging is not so trivial when your work flow is geared to replicate 
a CI/CD pipeline environment hosted on AWS with your local machine by containerizing 
an already containerized SAM application. 

This may solve inconistencies in your workflow when scaffolding some AWS SAM projects 
and attempting to parallel them on your local machine, however. Most modern companies
engaged in development should have definitions for these workflows and a means to promote 
code to production, but in a fast-paced tech wolrd seasoned developers have to come 
up with clever ways to isolate their environments and resources to provide stable 
testing platforms while establishments work their kinks out.

The workaround is Docker. We can encapsulate the build and test environments to
assure the local run will be the same as that within your CI/CD pipeline. However,
this becomes not so trivial when dealing with containerizing a SAM application, 
because under the hood SAM itself runs as a Docker container, and to get it to 
run in a parent Docker container is TRICKY, and confusing if you are new at 
containerizing for cloud deployments.

To compound the issue trying to use CI/CD tooling from AWS Codebuild for deploying 
required (just 7 months ago @Nov 2018) a bit of side work to make sure both your 
local build environment and Codebuild along with CodeDeploy services matched. 
Lambda may be better tied to this deployment process today and we will investigate 
a similar testing and deploy pipeline that we are outlining currently prior to
digging into AWS's repository for serverless applications. Services are advancing 
at remarkable rates regardless of the platform provider, so this provided solution
is an example of how to gear up for a new project 7 months later with similar 
requirements, both from a personal perspective and that from Monsoon Engineering.

## Solution by examples

I found an article that pretty much described in detail some points I encountered a
few months ago when learning to integrate a dev, test, and prod workflow together
with CodeDeploy and CodeBuild on a React project. Their solution is explained at:

https://medium.com/monsoon-engineering/running-aws-sam-in-a-docker-container-2491596672c2

The github repo for their dockerizing a SAM application is at:
https://github.com/monsooncommerce/monsoon-samples/tree/master/docker-sam

## Definition of the project example

The gist of this workaround is explained with a simple app that defines a node.js 
function to convert JSON input into a XML document using xml2json. It uses typscript,
a subset language of javascript with static type checking, and requires a dependency
addition and NPM to install and use the typescript compiler. The whole thing gets
bundled as a typescript application in a docker container. This is one "clever"
way to help assure yourself that local testing efforts are conguent and expected
with similar results when pushed through an automated deployment system, whether it
be on AWS or otherwise. 

## Coding the components



basic docker command to get it running:
```sh
docker-compose run --rm lambda_npm_app sh -c "npm install && npm run tsc"
```

Problems I initially faced paralleled this problem when rolling out my-portfolio 
in React a few months ago. It also dealt with mismatched environments between my 
prod site and dev testing pipelines. The lambda function I used actually was coded 
in python with an except clause to use the old build if the artifact bucket did not 
receive the results of the new push to github which initiated the AWS side build-
it just reverted back to a last used good build. Monsoons build did not seem to
encounter a node-gyp rebuild issue as mine did. I ended up building my project 
through yarn, as it provided a little more non-determinism at the time.

My concern was also how one goes about version management
with pip and the fact that AWS cli and SAM cli are separate, and the latter used
pip to install. Homebrew helped deal with a bit of that mystery for me, as I also
stepped into the MBP & Mojave world at the same time, thinking switching over to a
Mac would lessen the headache on the road to becoming a solutions architect, but 
thats for another day. 

Final thoughts are- trust your instincts. I just thought my problems were soley 
due to my own ignorance of the subject matter at the time which resulted in less than
efficienct testing flows (the course I took on React and AWS did not really use 
the built in Lambda function testing either). I used my time there to appreciate
Jest, Chai, and Mocha for React, and observed the tooling in AWS as a means to
the end of the project. I have some reconciliation that I knew there to be some 
validity to second guessing the environment setup and other issues I encountered
with NPM. The article from Moonsoon engineering help to solidify that. So if you 
were like me a few months ago its worth the 4 min read.

Anyway, back to CodeDeploy and CodeBuild- artifactory management was a little 
hairy to initially grasp within the pipeline- however as most know we can dictate 
some of the build parameters via the yaml and spec config files respectively, 
and now we have a better appreciation of what running a docker container in 
another abstracted SAM docker container really entails. Take a look at Kubernentes
and Jfrog as some alternatives to AWS, but we will try to revisit their resources
again to see what has changed since last fall.