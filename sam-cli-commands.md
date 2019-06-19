# SAM cli commands
Look a lot like docker. Link below will get you to the documenttion for flag 
options when using sam. Don't foget --help if you need to.

## cheat sheet command summary
sam build
  * Iterates through application
  * Serches for the manifest file, For Python it looks for requirements.txt
  * Creates artifacts to deploy to Lambda with package and deploy commands.
  * can build locally to test using 
  ```sh
  sam build && sam local invoke
  ```
sam deploy
  * command is an alias of aws cloudformation deploy
  > requires --template as the path for the SAM template file
  > requires --
## Documentation
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-command-reference.html
