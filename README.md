# My_CloudFormation_Templates_AWS
My customized AWS CloudFormation templates

## Working with AWS CLI

### 1. Validating a template
  * Template from your local environment
```bash
aws cloudformation validate-template --template-body file:///home/user/FileName.yaml
```
  * Template from an S3 Bucket
```bash
aws cloudformation validate-template --template-url https://s3.amazonaws.com/cloudformation-templates-us-east-1/S3_Bucket.template
```

### 2. Creating a Stack
  * Template from your local environment
```bash
aws cloudformation create-stack \
  --stack-name myteststack \
  --template-body file:///home/testuser/mytemplate.json \
  --parameters ParameterKey=Parm1,ParameterValue=test1 ParameterKey=Parm2,ParameterValue=test2
```
  * Template from an S3 Bucket
```bash
aws cloudformation create-stack \
  --stack-name myteststack \
  --template-url https://s3.amazonaws.com/cloudformation-templates-us-east-1/S3_Bucket.template \
  --parameters ParameterKey=Parm1,ParameterValue=test1 ParameterKey=Parm2,ParameterValue=test2
```
  * Stack in an AWS Systems Manager document
```bash
 aws cloudformation create-stack 
 --stack-name myteststack 
 --template-url "ssm-doc://arn:aws:ssm:us-east-1:123456789012:document/documentName"
```

### 3. Listing Stack Resources
```bash
aws cloudformation list-stack-resources --stack-name myteststack
```

### 4. Listing Stacks
```bash
aws cloudformation list-stacks
```
  * With filters
```bash
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE
```
  * Stack Status Filter can be:
`CREATE_COMPLETE` `CREATE_IN_PROGRESS` `CREATE_FAILED` `DELETE_COMPLETE` `DELETE_FAILED` `DELETE_IN_PROGRESS` `REVIEW_IN_PROGRESS` `ROLLBACK_COMPLETE` `ROLLBACK_FAILED` `ROLLBACK_IN_PROGRESS` `UPDATE_COMPLETE` `UPDATE_COMPLETE_CLEANUP_IN_PROGRESS` `UPDATE_FAILED` `UPDATE_IN_PROGRESS` `UPDATE_ROLLBACK_COMPLETE` `UPDATE_ROLLBACK_COMPLETE_CLEANUP_IN_PROGRESS` `UPDATE_ROLLBACK_FAILED` `UPDATE_ROLLBACK_IN_PROGRESS` `IMPORT_IN_PROGRESS` `IMPORT_COMPLETE` `IMPORT_ROLLBACK_IN_PROGRESS` `IMPORT_ROLLBACK_FAILED` `IMPORT_ROLLBACK_COMPLETE`

### 5. Describing Stacks
```bash
aws cloudformation describe-stacks --stack-name myteststack
```

### 6. Viewing Stack Event History
```bash
aws cloudformation describe-stack-events --stack-name myteststack
```

### 7. Retrieving a Template
```bash
aws cloudformation get-template --stack-name myteststack
```

### 8. Updating a Stack
```bash
aws cloudformation update-stack --stack-name myteststack --template-url https://s3.amazonaws.com/sample/updated.template
--parameters ParameterKey=VPCID,ParameterValue=SampleVPCID ParameterKey=SubnetIDs,ParameterValue=SampleSubnetID1\\,SampleSubnetID2
```
  * `Note`: This is done after the original template has been edited to include the expected changes, or with a different template. Changes are then made to the stack so named. The template can be retrieved using the 'get-template' command `aws cloudformation get-template --stack-name myteststack`.

### 9. Cancel an Update
```bash
aws cloudformation cancel-update-stack
```
  * `Note`: You can cancel only update stacks that are in the `UPDATE_IN_PROGRESS` state.

### 10. Rolling Back an Update
```bash
aws cloudformation continue-update-rollback --stack-name myteststack --resources-to-skip Resource_1 Resource_2
```
Other flags that can be passed with the `continue-update-rollback` can be found at  `https://docs.aws.amazon.com/cli/latest/reference/cloudformation/continue-update-rollback.html`

### 11. Deleting a Stack
```bash
aws cloudformation delete-stack --stack-name myteststack
```

## More information can be found in relevant AWS Documentations

