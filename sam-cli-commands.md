# SAM cli commands
Looks a lot like docker usage. In fact running --use-container can use a Lambda like 
docker container. We will expand on this momentarily. Link below will get you to the 
documenttion for flag options when using SAM. Don't foget --help if you need to.

## cheat sheet command summary
sam build
  * Iterates through application
  * Serches for the manifest file, for Python it looks for requirements.txt
  * Creates artifacts to deploy to Lambda with package and deploy commands
  * can build locally to test using 
  ```sh
  sam build && sam local invoke
  ```
  * Uses .aws-sam/build folder to write to your local workstation directory
  * For deployment we can do:
  ```sh
  sam build && sam package --s3-bucket <bucketname>
  ```
sam deploy
  * command is an alias of aws cloudformation deploy
  * requires --template as the path for the SAM template file
  * requires --

## Documentation
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-command-reference.html
