### Mappings
Mappings allow you to create a set of key-value pairs that you can reference in your CloudFormation template. Mappings can be used to specify values that depend on the region or the instance type, for example.

Here is an example of a Mappings section in a CloudFormation template:
```
Mappings:
  RegionMap:
    us-east-1:
      AMI: 'ami-12345678'
    us-west-2:
      AMI: 'ami-87654321'
```
In this example, the RegionMap mapping has two keys: us-east-1 and us-west-2. Each key has a value, which is an AMI ID.

To reference a value in a mapping, you can use the !FindInMap function:
```
Resources:
  MyInstance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: !FindInMap [RegionMap, !Ref 'AWS::Region', AMI]
```
The !FindInMap function takes three arguments: the mapping name, the key to look up, and the name of the value to return. In this example, the function will look up the AMI ID for the current region in the RegionMap mapping.

Conditions
Conditions allow you to specify when a resource or property should be created or included in a stack. Conditions are defined in the Conditions section of the template and can be referenced in the Resources or Outputs sections.

Here is an example of a Conditions section in a CloudFormation template:
```
Conditions:
  CreateProdResources: !Equals [!Ref Environment, prod]
```
This condition checks if the Environment parameter is equal to prod.

To use a condition in a resource or output, you can use the !If function:
```
Resources:
  ProdInstance:
    Type: 'AWS::EC2::Instance'
    Condition: CreateProdResources
    Properties:
      ImageId: 'ami-12345678'
      InstanceType: 't2.micro'

Outputs:
  ProdInstanceId:
    Value: !Ref ProdInstance
    Condition: CreateProdResources
```
In this example, the ProdInstance resource and the ProdInstanceId output will only be created if the CreateProdResources condition is true.

Logical Functions
CloudFormation provides several functions that allow you to perform logical operations in your templates. These functions include:

!And: Returns true if all the specified conditions are true, and false otherwise.
!Or: Returns true if at least one of the specified conditions is true, and false otherwise.
!Not: Returns the logical opposite of a condition. If the condition is true, !Not returns false, and vice versa.
Here is an example of how to use the !And function:
```
Conditions:
  CreateResources: !And [Condition1, Condition2
```
