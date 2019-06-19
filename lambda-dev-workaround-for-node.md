# The problem
Containerizing serverless node.js applications in AWS for testing locally on your
machine is not as easy as deploying a serverless application with Lambda. SAM cli
is used to package and run your Lambda function locally. To compound the issue
trying to use CI/CD tooling from AWS Codebuild for deploying required (just 6 
months ago @Nov 2018) a bit of side work to make sure both your local build 
environment and that used within your AWS account through CodeBuild matched.

The workaround is Docker. We can encapsulate the build and test environments to
assure the local run will be the same as that within your CI/CD pipeline. However,
this becomes not so trivial when dealing with containerizing a SAM application, 
because under the hood SAM itself runs as a Docker container, and to get it to 
run in a parent Docker container is TRICKY, and confusing if you are new at 
containerizing for cloud deployments.

I found an article that pretty much described all the points I had trouble with a
few months ago when learning to integrate a dev, test, and prod workflow together
with CodeDeploy and CodeBuild. Their github explination of dockerizing a SAM 
application is at https://github.com/monsooncommerce/monsoon-samples/tree/master/docker-sam

The gist of their workaround example is explained with a simple app that defines a node.js 
function to convert JSON input into a XML document using xml2json. It uses typscript,
a subset language of javascript with static type checking, and requires a dependency
addition and NPM to install and use the typescript compiler. The whole thing gets
bundled as a typescript application in a docker container.

-----------will get back to this part after fixing a flat on my car----------

Problems I initially faced paralleled this problem when rolling out my-portfolio 
in React a few months ago. It also dealt with mismatched environments between my 
prod site and dev testing pipelines. The lambda function actually was coded in 
python with an except clause to use the old build if the artifact bucket did not 
receive the results of the new push to github which initiated the AWS side build-
it just reverted back to a last used good build. 

My concern was also how one goes about version management
with pip and the fact that AWS cli and SAM cli are separate, and the latter used
pip to install. Homebrew helped deal with a bit of that mystery for me, as I also
stepped into the MBP & Mojave world at the same time, thinking switching over to a
Mac would lessen the headache on the road to becoming a solutions architect, but 
thats for another day. I just thought it was due to my own ignorance of the subject 
matter at the time that resulted in poorly executed testing flows, along side a 
not so comprehensive test button usage directly in the Lambda console, but I have
some reconciliation that I knew there to be some validity to second guessing 
environment setup, semver issues with NPM, and the like, with this article I found
from monsoon engineering. So if you were like me a few months ago its worth the 4 min
read:

https://medium.com/monsoon-engineering/running-aws-sam-in-a-docker-container-2491596672c2

Anyway, back to CodeBuild- artifactory management was a little 
hairy within the pipeline, however as most know we can dictate some of the build 
parameter via the yaml and spec configs file, and now we have a better appreciation
of what running a docker container in another docker container really entails.