To build a Kubernetes cluster using AWS CloudFormation, you can use the AWS::EKS::Cluster resource in your CloudFormation template. This resource creates an Amazon Elastic Container Service for Kubernetes (Amazon EKS) cluster in your AWS account. Here's an example of how you could define the AWS::EKS::Cluster resource in your CloudFormation template:

```
Resources:
  MyEKSCluster:
    Type: AWS::EKS::Cluster
    Properties:
      Name: my-eks-cluster
      Version: 1.18
      EncryptionConfig:
        - Provider: aws
          KeyArn: arn:aws:kms:us-west-2:123456789012:key/12345678-1234-1234-1234-123456789012
```

This will create an EKS cluster with the name my-eks-cluster and version 1.18. You can specify a different name and version as needed.

Once the EKS cluster has been created, you can use it to deploy the Moodle application by creating a Kubernetes Deployment resource in your CloudFormation template. Here's an example of how you could define a Deployment resource in your template:

```
Resources:
  MyMoodleDeployment:
    Type: AWS::EKS::Deployment
    Properties:
      ClusterName: !Ref MyEKSCluster
      ServiceName: my-moodle-service
      DesiredCount: 2
      Template:
        Resources:
          # Define your Moodle pods and other resources here

```

This will create a Deployment with the name my-moodle-deployment that runs two replicas of the Moodle application. You will need to define the Moodle pods and other resources in the Template property of the Deployment resource.

I hope this helps! Let me know if you have any questions or need further assistance.
