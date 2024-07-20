aws cloudformation create-stack --stack-name bedrock-workshop --capabilities CAPABILITY_NAMED_IAM --template-body file://cf.yml --tags Key=Name,Value=BedrockWorkshop --region <AWS REGION>

- Below resources will be created
  - in S3 bucket with the name bedrock-workshop-xxxxxxxx.
  - A VPC with two public subnets and two private subnets, with a security group called BedrockWorkshopSecurityGroup
  - An IAM role with the name AmazonBedrockWorkshopStackSageMakerRole, attached required policy. The IAM role allows AssumeRole to be used by the SageMaker service.
  - An IAM role with the name AmazonBedrockWorkshopStackLambdaFunctionRole, attached required policy. The IAM role allows AssumeRole by the Lambda function service.
  - An IAM role with the name AmazonBedrockWorkshopStackKnowledgeBaseRole, with the required IAM policy. The IAM role allows AssumeRole by the Bedrock service.
  - An IAM role with the name AmazonBedrockWorkshopStackAgentRole, with the required IAM policy. The IAM role allows AssumeRole by the Bedrock service
  - An IAM role with the name AmazonBedrockWorkshopStackActionGroupLambdaFunctionRole, with the required IAM policy. The IAM role allows AssumeRole by the Lambda function service.
  - An RDS PostgreSQL instance
  - A set of Secrets Manager secrets, which contains the database connection credentials for the RDS PostgreSQL instance
  - A SageMaker Domain with a user profile.
  - An API Gateway as the front end for Lambda function BedrockWorkshopChatbot.
  - A Lambda function BedrockWorkshopActionGroup
 
    ![image](https://github.com/user-attachments/assets/fa1c0b55-12db-4c07-aff6-cf9eb4211dc4)

  
