![](https://codebuild.us-east-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiN2FvM2QzZnBCK1JjZjBTajQ5R0JlazZhOGo3c2toQktFRzVKNDNENlZ1YUU3Y1kyeEdkU2VTOGZxVllMVzh0UG9oeHBXM0Y0VGVrVloyYmUzSFNacjdRPSIsIml2UGFyYW1ldGVyU3BlYyI6InNUT3lrYmNpOVhsS2Q0aXIiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

## aws-sam-cfnresponse

This repo utilizes the Serverless Application Model (SAM) to create a lambda layer via codebuild. The codebuild project utilizes a buildspec.yml to specify what packages to put into the lambda layer. After SAM builds the lambda layer it is then pushed to an s3 bucket and uploaded the layer to the lambda layers. Each subsequent build will automatically increment the lambda layer version for you. Logs for the codebuild project will be created in CloudWatch with the following naming convention: aws/codebuild/\<codebuild-project-name\>

### buildspec.yml

The buildspec.yml builds the lambda layer via AWS Codebuild.

### IAM Role creation and Codebuild Project

The codebuild.yml creates the IAM Role and the Codebuild project. The IAM Role needs permissions for s3, codebuild, cloudformation, lambda and IAM. The codebuild project utilizes the buildspec.yml located in the github repository to build. 

#### Repository Structure

```bash
aws-sam-cfnresponse/
├── .gitignore
├── README.md
├── buildspec.yml
├── codebuild.yml
├── template.yaml
├── python-layer/
    ├── requirements.txt
```
##### References:

https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-layerversion.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/building-layers.html
https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html#build-spec-ref-example
