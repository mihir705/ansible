# ansible

Job-ready Ansible repo: core concepts as hands-on labs, reusable roles, and cloud playbooks that mirror `/Users/mihir/code/terraform-aws`, `terraform-azure`, `terraform-gcp` (and the OpenTofu counterparts).

Playbooks are the runbooks. Roles are the reusable modules. Extra-var maps (`vars/*.yml`) are the equivalent of `terraform.tfvars` — omit any map you are not managing.

## Structure

```
ansible/
├── ansible.cfg
├── requirements.yml
├── inventories/
│   ├── lab/hosts.yml              # localhost lab
│   └── prod/
│       ├── hosts.yml              # SSH inventory
│       └── aws_ec2.yml            # dynamic inventory plugin
├── group_vars/  host_vars/
├── vault/secrets.yml.example
├── roles/                         # like terraform modules
│   ├── common/
│   ├── users/
│   ├── packages/
│   ├── nginx/
│   ├── docker/
│   ├── postgresql/
│   └── harden/
├── playbooks/
│   ├── site.yml                   # environment entrypoint
│   ├── ping.yml  facts.yml  web.yml  db.yml  docker.yml  harden.yml
│   ├── rolling.yml
│   └── cloud/aws.yml azure.yml gcp.yml
├── vars/*.yml.example             # like terraform.tfvars.example
├── labs/00-setup … 12-ci          # concept curriculum
└── environments/prod/
```

## Curriculum (do in order)

| Lab | Concepts |
|-----|----------|
| [00-setup](labs/00-setup/README.md) | Install Ansible, collections, inventory graph |
| [01-adhoc-and-inventory](labs/01-adhoc-and-inventory/README.md) | Ad-hoc, groups, patterns |
| [02-playbooks-and-modules](labs/02-playbooks-and-modules/README.md) | Play, task, FQCN, idempotency, check mode |
| [03-variables-facts-vault](labs/03-variables-facts-vault/README.md) | group_vars, precedence, facts, ansible-vault |
| [04-conditionals-loops-handlers](labs/04-conditionals-loops-handlers/README.md) | `when`, `loop`, `notify` |
| [05-templates-and-jinja2](labs/05-templates-and-jinja2/README.md) | `template`, filters |
| [06-roles-and-galaxy](labs/06-roles-and-galaxy/README.md) | Role layout, collections |
| [07-blocks-tags-error-handling](labs/07-blocks-tags-error-handling/README.md) | block/rescue/always, tags, `failed_when` |
| [08-dynamic-inventory](labs/08-dynamic-inventory/README.md) | AWS EC2 inventory plugin |
| [09-aws-hands-on](labs/09-aws-hands-on/README.md) | amazon.aws vs terraform-aws |
| [10-azure-hands-on](labs/10-azure-hands-on/README.md) | azure.azcollection vs terraform-azure |
| [11-gcp-hands-on](labs/11-gcp-hands-on/README.md) | google.cloud vs terraform-gcp |
| [12-ci-check-mode-lint](labs/12-ci-check-mode-lint/README.md) | `--check --diff`, ansible-lint |

Also covered in playbooks: rolling updates (`playbooks/rolling.yml`, `serial`), privilege escalation (`become`), and limiting hosts (`--limit`).

## How it works (same idea as Terraform/OpenTofu)

| Ansible | Terraform / OpenTofu |
|---------|----------------------|
| `roles/` | `modules/` |
| `playbooks/site.yml` | `environments/prod/main.tf` |
| `inventories/prod` | backend + workspace/env |
| `vars/aws.yml` maps | `terraform.tfvars` blocks |
| `ansible-playbook --check` | `tofu plan` |
| `ansible-playbook` | `tofu apply` |
| `--tags` / `--limit` | `-target` |
| ansible-vault | secret values kept out of git |

| `vars/*.yml` block | Playbook / collection module |
|--------------------|------------------------------|
| `vpcs` | `amazon.aws.ec2_vpc_net` / GCP network |
| `buckets` | `amazon.aws.s3_bucket` |
| `security_groups` | `amazon.aws.ec2_security_group` |
| `ec2_instances` | `amazon.aws.ec2_instance` |
| `resource_groups` | `azure.azcollection.azure_rm_resourcegroup` |
| `storage_accounts` | `azure.azcollection.azure_rm_storageaccount` |
| `virtual_networks` | `azure.azcollection.azure_rm_virtualnetwork` |
| `cloud_storage_buckets` | `google.cloud.gcp_storage_bucket` |

Linux roles (`nginx`, `docker`, `postgresql`, `harden`) cover the day-two work Terraform does not: packages, services, templates, users, SSH hardening.

## Quick start (lab on localhost)

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install 'ansible-core>=2.16' ansible-lint
ansible-galaxy collection install -r requirements.yml

ansible-inventory --graph
ansible-playbook playbooks/ping.yml
ansible-playbook labs/02-playbooks-and-modules/hello.yml
ansible-playbook playbooks/web.yml --check
```

Work through `labs/00-setup` → `labs/12-ci-check-mode-lint`. Cloud labs need AWS/Azure/GCP credentials; omit unused maps in `vars/*.yml` before applying.

## Apply one layer at a time

```bash
ansible-playbook playbooks/ping.yml
ansible-playbook playbooks/web.yml --tags web
ansible-playbook playbooks/db.yml --limit db1
ansible-playbook playbooks/site.yml --tags harden --check
ansible-playbook -i inventories/prod/hosts.yml playbooks/site.yml --limit web1
```

Never commit `vault/secrets.yml` or real cloud keys.
