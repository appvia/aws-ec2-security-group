# aws-ec2-security-group

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 4.8.0](https://img.shields.io/badge/AppVersion-4.8.0-informational?style=flat-square)

AWS EC2-VPC Security Group Helm chart for the [Terraform-operator](https://github.com/isaaguilar/terraform-operator).

## Prerequisites
```bash
helm repo add isaaguilar https://isaaguilar.github.io/helm-charts
helm repo update
helm upgrade --install terraform-operator isaaguilar/terraform-operator \
  --version v0.2.1 --namespace tf-system --create-namespace
```

## Get Repo Info
```bash
helm repo add appvia-community https://appvia-community.storage.googleapis.com
helm repo update
helm search repo appvia-community
```

## Install Chart
```bash
helm install [RELEASE_NAME] appvia-community/aws-ec2-security-group \
  --namespace [NAMESPACE] \
  --create-namespace \
  --set aws.region=[AWS_REGION] \
  --set aws.credentials=[AWS_CREDENTIALS] \
  --set ec2.sg_name=[AWS_EC2_SG_NAME] \
  --set ec2.vpc_id=[AWS_EC2_VPC_ID]
```

## Upgrade Chart
```bash
helm upgrade --install [RELEASE_NAME] appvia-community/aws-ec2-security-group \
  --namespace [NAMESPACE] \
  --create-namespace \
  --set aws.region=[AWS_REGION] \
  --set aws.credentials=[AWS_CREDENTIALS] \
  --set ec2.sg_name=[AWS_EC2_SG_NAME] \
  --set ec2.vpc_id=[AWS_EC2_VPC_ID]
```

## Uninstall Chart
```bash
helm uninstall [RELEASE_NAME]
```

## Example Usage
```bash
helm upgrade --install aws-ec2-security-group appvia-community/aws-ec2-security-group \
  --namespace my-ns \
  --set aws.region=eu-west-2  \
  --set ec2.sg_name=my-sg \
  --set ec2.vpc_id=vpc-470c442f \
  --set aws.credentials[0].secretNameRef.key=data,aws.credentials[0].secretNameRef.name=tf-aws-secrets,aws.credentials[0].secretNameRef.namespace=my-ns
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| aws.credentials | object | `{}` | The AWS credentials to be used for provisioning the IAM role. See [supported credential types](http://tf.isaaguilar.com/docs/references/configuration/#credentials-v1alpha1-tf) |
| aws.region | string | `""` | The AWS region where the IAM role should be created |
| ec2.ingress_with_cidr_blocks | list | `[]` | List of ingress rules to create where 'cidr_blocks' is used [MUTABLE]|
| ec2.sg_name | string | `""` | Name of EC2-VPC Security Group [IMMUTABLE] |
| ec2.vpc_id | string | `""` | ID of the VPC where to create security group [IMMUTABLE] |
| terraform.module | string | `"https://github.com/terraform-aws-modules/terraform-aws-security-group"` | The HashiCorp official Terraform module |
| terraform.moduleVersion | string | `"v4.8.0"` | The version of the Terraform module used to create an IAM role |
| terraform.version | string | `"1.1.4"` | The version of Terraform used |

:warning: A change to an `IMMUTABLE` parameter after initial creation will force a re-creation of the AWS EC2-VPC security group. However a `MUTABLE` parameter is a configurable option by design and can be changed.

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.7.0](https://github.com/norwoodj/helm-docs/releases/v1.7.0)
