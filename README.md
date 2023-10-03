# Export your Account ID
```
export ACCOUNT_ID=617729733308
```
# Set Trust Policy
```
TRUST="{ \"Version\": \"2012-10-17\", \"Statement\": [ { \"Effect\": \"Allow\", \"Principal\": { \"AWS\": \"arn:aws:iam::${ACCOUNT_ID}:root\" }, \"Action\": \"sts:AssumeRole\" } ] }"
```
# Verify inside Trust policy, your account id got replacd
```
echo $TRUST
```

# First create a new file NewRoleTrustPolicy.json with the following contents:
```
{

"Version": "2012-10-17",

"Statement": [

{

"Sid": "",

"Effect": "Allow",

"Principal": {

"AWS": "arn:aws:iam::xxxxxxxxxxxx:root"

},

"Action": "sts:AssumeRole"

}

]

}
```
Note: please replace your account ID in the above Principal parameter.
```
New-IAMRole -AssumeRolePolicyDocument (Get-Content -raw NewRoleTrustPolicy.json) -RoleName EksCodeBuildKubectlRole
```
# Note Above command work on only powershell 

New-IAMRole -AssumeRolePolicyDocument (Get-Content -raw NewRoleTrustPolicy.json) -RoleName EksCodeBuildKubectlRole

```
{ "Version": "2012-10-17",

"Statement":

[ { "Effect": "Allow",

"Action": "eks:Describe*",

"Resource": "*" }

]
}
```
Write-IAMRolePolicy -RoleName EksCodeBuildKubectlRole -PolicyName eks-describe -PolicyDocument (Get-Content -Raw iam-eks-describe-policy.json)
