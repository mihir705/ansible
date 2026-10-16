# Lab 09 — AWS hands-on

Maps to `/Users/mihir/code/terraform-aws` and `opentofu-aws`. Ansible uses `amazon.aws` instead of HCL modules.

| Terraform tfvars | Ansible vars map | Module |
|------------------|------------------|--------|
| `vpcs` | `vpcs` | `amazon.aws.ec2_vpc_net` |
| `security_groups` | `security_groups` | `amazon.aws.ec2_security_group` |
| `buckets` | `buckets` | `amazon.aws.s3_bucket` |
| `ec2_instances` | `ec2_instances` | `amazon.aws.ec2_instance` |

```bash
cp vars/aws.yml.example vars/aws.yml
# edit names so they are globally unique (S3)
ansible-playbook playbooks/cloud/aws.yml --check
# remove unused maps before a real apply, same idea as omitting tfvars blocks
ansible-playbook playbooks/cloud/aws.yml
```

Auth: `aws configure` or environment variables. Never commit keys.
