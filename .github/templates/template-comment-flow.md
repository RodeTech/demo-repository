## GitHub Actions Pull Request commands (comment flow):

### To use these commands, please add them in the comments of the Pull Request
<details><summary>Click to expand</summary>

- To run **terragrunt plan** for all changed terragrunt.hcl files write in the comments:
```sh
tg plan
```

- To run **terragrunt plan** for specific terragrunt.hcl file (optional with target resource) write in the comments:
```sh
tg plan --path=<path to terragrunt.hcl> # indrive-dev/eu-central-1/dev/services/dmtest/cloudfront/alarms/terragrunt.hcl
tg plan --path=<path to terragrunt.hcl> --target=<resource in state> # aws_eks_cluster.this[0]
```

- To run **terragrunt apply** for all successfully planned terragrunt.hcl files write in the comments:
```sh
tg apply
```

- To run **terragrunt apply** for specific terragrunt.hcl file (optional with target resource) write in the comments:
```sh
tg apply --path=<path to terragrunt.hcl> # indrive-dev/eu-central-1/dev/services/dmtest/cloudfront/alarms/terragrunt.hcl
tg apply --path=<path to terragrunt.hcl> --target=<resource in state> # aws_eks_cluster.this[0]
```

- To run **terragrunt apply** for all resources regardless of successfull plan terragrunt.hcl files write in the comments:
```sh
tg apply all
```

- To run **terragrunt destroy** for all **DELETED** terragrunt.hcl files write in the comments:
```sh
tg destroy
```

- To run **terragrunt state list** for specific terragrunt.hcl file write in the comments:
```sh
tg state list --path=<path to terragrunt.hcl> # indrive-dev/eu-central-1/dev/services/dmtest/cloudfront/alarms/terragrunt.hcl
```

- To run **terragrunt state rm** for specific terragrunt.hcl file write in the comments:
```sh
tg state rm
  --path=<path to terragrunt.hcl> # indrive-dev/eu-central-1/dev/services/dmtest/cloudfront/alarms/terragrunt.hcl
  --resource=<resource in state> # module.metric-alarm["alarm_cloudfront_5xxErrorRate"].aws_cloudwatch_metric_alarm.this[0]
```

- To run **terragrunt import** for specific terragrunt.hcl file write in the comments:
```sh
tg import
  --path=<path to terragrunt.hcl> # indrive-dev/eu-central-1/dev/services/dmtest/cloudfront/alarms/terragrunt.hcl
  --to=<resource in state> # module.metric-alarm["alarm_cloudfront_5xxErrorRate"].aws_cloudwatch_metric_alarm.this[0]
  --id=<resource in AWS> # You can find the explanation below.
```

<details><summary>Constructing the tg import command for Terraform resources</summary>

The `tg import` command allows you to associate Terraform-managed resources with existing infrastructure components. Each command follows the pattern:

```sh
tg import
  --path=FILE_PATH
  --to=RESOURCE_TYPE.RESOURCE_NAME[INDEX]
  --id=RESOURCE_ID
```

1. **FILE_PATH**: The relative path to the `terragrunt.hcl` file that manages this resource.

2. **RESOURCE_TYPE**: The type of resource you are importing, which follows the Terraform resource naming convention. For example:

- AWS Security Group: `aws_security_group`
- AWS S3 Bucket: `aws_s3_bucket`
- AWS RDS Instance: `aws_db_instance`

3. **RESOURCE_NAME**: The logical name of the resource in the Terraform configuration. This is the name you have assigned in the `.tf` file. For example, look into `tg output`:

```sh
### Plan for indrive-prod-devplatform/eu-north-1/devplatform/shared/redis-7-auth-test/redis7/users/terragrunt.hcl:
...
  # aws_elasticache_user_group.this[0] has changed
```

- `aws_elasticache_user_group.this[0]` will be the resource
- `[0]` is the index

> **INDEX**: This applies when you are importing resources from lists or modules where multiple instances of the resource exist. If there is only one resource, you can omit the index. If there are multiple, use [INDEX] to specify which resource you want to import (starting from [0] for the first resource).

4. **RESOURCE_ID**: The ID of the resource in your cloud provider’s infrastructure. For AWS, this is usually an identifier like:
- Security Group: `sg-09a43826e5f63b24f`
- S3 Bucket: `my-s3-bucket`
- RDS Instance: `rds-instance-id`

> Or you can find it into terraform docs (just google the resource name and in the document bottom it will be resource id selection, [example](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group#import)).

</details>

</details>

### Warnings

<details><summary>Click to expand</summary>

> The commands cannot be used in a merged Pull Request.

> The `tg apply/tg apply all/tg destroy` commands can be used only after approval.

> If a resource has many dependencies (e.g. ElastiCache), the plan may fail during deployment. Therefore, each time you run the tg plan / tg apply command, the comment from the github-actions bot will show new output. You may need to write the command multiple times to deploy a resource with dependencies.

> To delete a resource, you need to comment with `tg destroy` and remove the files from the repository in the PR itself.

</details>
