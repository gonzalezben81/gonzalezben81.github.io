##Created AWS Resources

Before you configure the HCP Vault AWS auth method, you must create the necessary resources in AWS. The AWS auth method will require an IAM policy that permits the appropriate access for the auth method, an IAM user with programmatic access, and one or more roles that you will assign to other AWS services that require authentication to Vault.

##Create IAM Policy

You will now create the IAM policy for your IAM User

``` json
{
"Version": "2012-10-17",
"Statement": [
 {
   "Effect": "Allow",
   "Action": [
     "ec2:DescribeInstances",
     "iam:GetInstanceProfile",
     "iam:GetUser",
     "iam:ListRoles",
     "iam:GetRole"
   ],
   "Resource": "*"
 }
 ]
}


```

##Create connection to Vault via AWS User


Enable aws auth on your vault instance.

``` bash
vault auth enable aws

```

Check to see if the vault auth aws method has been enabled.

``` bash
vault auth list

```

Next connect the IAM role you created in AWS to the Vault aws auth backend. This will configure the aws auth method with access to your AWS account using the Access key ID and Secret Access Key previously created for the IAM User you created in AWS.

``` bash

vault write auth/aws/config/client secret_key=<secret-key> access_key=<access-key>

```


##Create Vault role for connection to AWS IAM Role

Configure the aws auth method to trust the AWS IAM role previously created and attach the vault-policy-for-aws-ec2role to the token provided by the aws auth method. Replace <iam-arn> with the actual IAM Role arn you created in AWS.

```
vault write auth/aws/role/vault-role-for-aws-ec2role \
     auth_type=iam \
     bound_iam_principal_arn=<iam-arn> \
     policies=default,allinonepolicy
```


```
vault write auth/approle/role/vault-role-for-aws-ec2role \
    secret_id_ttl=10m \
    token_num_uses=0 \
    token_ttl=20m \
    token_max_ttl=30m \
    secret_id_num_uses=40
```    

List the roles you creates for the aws auth method

```
vault list /auth/aws/role
```

```
vault write auth/aws/role/vaultauth auth_type=iam \
              bound_iam_principal_arn=<iam-arn> policies=default,allinonepolicy max_ttl=500h
```          
