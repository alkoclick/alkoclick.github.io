# Authenticating into AWS ECR
Authentication command: 
`$(aws-vault exec PROFILENAME -- aws ecr get-login-password)`

or

`aws-vault exec PROFILENAME -- aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin ECRPATH.amazonaws.com`

The no-include-email is required because [docker has deprecated the email switch](https://github.com/awslabs/amazon-ecr-credential-helper/issues/51) but the aws cli hasn't caught up

#aws #containers #docker