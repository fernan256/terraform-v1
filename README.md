# Terraform

## AWS Key Pairs

One of the most common issues reported by people is confusion over AWS Key Pairs and Regions.  The Terraform configurations make use of us-east-1 (N. Virginia) as the default region.  You can override that region by changing the default or submitting a different value for `var.region`.  The AWS Key Pair you use must be created in the same region you have selected for deployment.  You can create those keys from either the AWS EC2 Console or the AWS CLI.  If you are using the CLI, the process is very simple.

```console
aws configure set region your_region_name
aws ec2 create-key-pair --key-name your_key_name
```

The json output will include a KeyMaterial section.  Copy and paste the contents of the KeyMaterial section starting with `-----BEGIN RSA PRIVATE KEY-----` and ending with `-----END RSA PRIVATE KEY-----` to a file with a .pem extension.  Then point the *tfvars* entry for `private_key_path` to the full path for the file.

If you are using Windows, remember that the file path backslashes need to be doubled, since the single backslash is the escape character for other special characters.  For instance, the path `C:\Users\Ned\mykey.pem` should be entered as `C:\\Users\\Ned\\mykey.pem`.