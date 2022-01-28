# AWS CloudFormation Learnings
Contains notes on the different things I learned and best practices in using CloudFormation

**TAGS**
Always add tags to your resources. Would be good if the tag values are parameterized, so that it's easier to change it later on, without updating the actual template.

AWS CloudFormation also has an option to add tags when you're configuring the stack options. The tags that you specify here will be applied to all resources in your stack. You can add up to 50 unique tags for each stack. However, there are some AWS services that don't "inherit" the tags that you place in the stack options. Here are those resources I have encountered so far:

AWS::CertificateManager::Certificate
AWS::Cognito::UserPool

