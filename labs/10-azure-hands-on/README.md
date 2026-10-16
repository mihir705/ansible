# Lab 10 — Azure hands-on

Maps to `/Users/mihir/code/terraform-azure` and `opentofu-azure`.

| Terraform tfvars | Ansible vars map | Module |
|------------------|------------------|--------|
| `resource_groups` | `resource_groups` | `azure.azcollection.azure_rm_resourcegroup` |
| `storage_accounts` | `storage_accounts` | `azure.azcollection.azure_rm_storageaccount` |
| `vnets` | `virtual_networks` | `azure.azcollection.azure_rm_virtualnetwork` |

```bash
az login
cp vars/azure.yml.example vars/azure.yml
ansible-playbook playbooks/cloud/azure.yml --check
ansible-playbook playbooks/cloud/azure.yml
```
