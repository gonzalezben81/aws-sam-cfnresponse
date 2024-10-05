![](https://codebuild.us-east-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiN2FvM2QzZnBCK1JjZjBTajQ5R0JlazZhOGo3c2toQktFRzVKNDNENlZ1YUU3Y1kyeEdkU2VTOGZxVllMVzh0UG9oeHBXM0Y0VGVrVloyYmUzSFNacjdRPSIsIml2UGFyYW1ldGVyU3BlYyI6InNUT3lrYmNpOVhsS2Q0aXIiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

### aws-sam-cfnresponse

This repo utilizes the Serverless Application Model (SAM) to create a lambda layer via codebuild. The codebuild project utilizes a buildspec.yml to specify what packages to put into the lambda layer. After SAM builds the lambda layer it is then pushed to an s3 bucket and uploads the layer to the lambda layers. Each subsequent build will automatically increment the lambda layer version for you. Logs for the codebuild project will be created in CloudWatch with the following naming convention: aws/codebuild/\<codebuild-project-name\>

### buildspec.yml

The buildspec.yml builds the lambda layer via AWS Codebuild. The currenty runtime utilized python3.9 and you can specify the runtime version you would like via `runtime-versions` in the buildspec.yml. Currently there is no s3 bucket specified in the builspec.yml. The AWS sam build, package, and deploy commands help with building the zip file for the lambda layer.

```Note
sam deploy now implicitly performs the functionality of sam package. You can use the sam deploy command directly to package and deploy your application.

Reference: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-package.html
```

### requirements.txt

The requirements.txt is where you will specify what python packages to install in the lambda layer. There is a size limit of 250MB for a lambda layer and function unzipped. Therefore only install the necessary layers

### IAM Role creation and Codebuild Project

The codebuild.yml creates the IAM Role and the Codebuild project. The IAM Role needs permissions for s3, codebuild, cloudformation, lambda and IAM. The codebuild project utilizes the buildspec.yml located in the github repository to build. 

#### Repository Structure

```bash
aws-sam-cfnresponse/
├── python-layer/
    ├── requirements.txt
├── README.md
├── buildspec.yml
├── codebuild.yml
├── template.yaml
```
##### References:

+ AWS::Serverless::LayerVersion CF Reference: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-layerversion.html
+ Building Lambda layers in AWS SAM: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/building-layers.html
+ Buildspec example: https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html#build-spec-ref-example
+ Lambda Layers: https://docs.aws.amazon.com/lambda/latest/dg/chapter-layers.html
+ Lambda Layers SAM: https://docs.aws.amazon.com/lambda/latest/dg/layers-sam.html
+ Lambda Layer Sample Apps: https://github.com/awsdocs/aws-lambda-developer-guide/tree/main/sample-apps/layer-python
+ sam build: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-build.html
+ sam package: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-package.html
+ sam deploy: https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-cli-command-reference-sam-deploy.html
+ CodeBuild Badges: https://docs.aws.amazon.com/codebuild/latest/userguide/publish-badges.html

