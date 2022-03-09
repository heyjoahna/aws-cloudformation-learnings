# AWS CloudFormation Learnings
Contains notes on the different things I learned and best practices in using CloudFormation. This is a live document and will be updated every now and then.

## PARAMETERS
- **Pseudo parameters**
  - Use CloudFormation [pseudo parameters](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/pseudo-parameter-reference.html) to make your templates more reusable

## RESOURCES
- **AWS Certificate Manager**
  - AWS::CertificateManager::Certificate
    - In ValidationMethod, use DNS method as much as possible so that domain validation is handled automatically. Note though that this will only happen if (a) the certificate domain is hosted in Amazon Route 53 and (b) the domain resides in your AWS account.

- **Amazon EventBridge**
  - AWS::Events::Rule
    - Tags is an unsupported property

- **Amazon RDS**
  - AWS::RDS::DBCluster
    - For EngineMode: serverless, when you update any parameter in your AWS::RDS::DBCluster, there will be an error regarding *PreferredBackupWindow* and *PreferredMaintenanceWindow* when you redeploy your stack:
      - _**You currently can't modify BackupWindow with Aurora Serverless**_ or _**Currently can't modify MaintenanceWindow with Aurora Serverless**_
      - This happens even though you haven't changed the PreferredBackupWindow and PreferredMaintenanceWindow properties
      - Workaround for this [issue](https://github.com/aws-cloudformation/cloudformation-coverage-roadmap/issues/396) is to remove (or comment out) the PreferredBackupWindow and PreferredMaintenanceWindow properties from the template and then rerun your stack


## TAGS
Always add tags to your resources. Would be good if the tag values are parameterized, so that it's easier to change it later on, without updating the actual template.

AWS CloudFormation also has an option to add tags when you're configuring the stack options. The tags that you specify here will be applied to all resources in your stack. You can add up to 50 unique tags for each stack. However, there are some AWS services that don't "inherit" the tags that you place in the stack options. Here are those resources I have encountered so far:
- AWS::CertificateManager::Certificate
- AWS::Cognito::UserPool
- AWS::Events::Rule
- AWS::IAM::ManagedPolicy

