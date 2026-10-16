# Lab 11 — GCP hands-on

Maps to `/Users/mihir/code/terraform-gcp` and `opentofu-gcp`.

| Terraform tfvars | Ansible vars map | Module |
|------------------|------------------|--------|
| `cloud_storage_buckets` | `cloud_storage_buckets` | `google.cloud.gcp_storage_bucket` |
| `vpcs` | `vpcs` | `google.cloud.gcp_compute_network` |

```bash
gcloud auth application-default login
cp vars/gcp.yml.example vars/gcp.yml
ansible-playbook playbooks/cloud/gcp.yml --check
ansible-playbook playbooks/cloud/gcp.yml
```
