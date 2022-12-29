To build an SFTP server using AWS CloudFormation, you can use the AWS::Transfer::Server resource. 
This resource allows you to create an SFTP server that you can use to securely transfer files to and from the server using SFTP.

Here is an example CloudFormation template that creates an SFTP server:
```
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MySFTP:
    Type: AWS::Transfer::Server
    Properties:
      Certificate:
        CertificateBody: |
          -----BEGIN CERTIFICATE-----
          # Your certificate goes here
          -----END CERTIFICATE-----
        CertificateChain: |
          -----BEGIN CERTIFICATE-----
          # Your certificate chain goes here
          -----END CERTIFICATE-----
        PrivateKey: |
          -----BEGIN RSA PRIVATE KEY-----
          # Your private key goes here
          -----END RSA PRIVATE KEY-----
      EndpointDetails:
        AddressAllocationIds:
          - eipalloc-xxxxxxxx
        SubnetIds:
          - subnet-xxxxxxxx
          - subnet-xxxxxxxx
        SecurityGroupIds:
          - sg-xxxxxxxx
      IdentityProviderType: SERVICE_MANAGED
      LoggingRole: arn:aws:iam::xxxxxxxxxxxx:role/transfer-service-role
      Tags:
        - Key: Name
          Value: MySFTP
```

In this example, the MySFTP resource creates an SFTP server with a certificate, certificate chain, and private key that you provide. 
The server is placed in the specified subnets and security group, and it uses the SERVICE_MANAGED identity provider type, 
which means that the SFTP server will manage its own user authentication. 

Finally, the LoggingRole property specifies the IAM role that the SFTP server will use to write log events to Amazon CloudWatch.

You can also customize the SFTP server by specifying additional properties, such as the maximum number of users that can connect to the server at the same time, or the default file transfer settings for users who connect to the server.

For more information about the AWS::Transfer::Server resource and how to use it in CloudFormation templates, see the AWS::Transfer::Server documentation.
