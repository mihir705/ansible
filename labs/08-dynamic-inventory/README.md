# Lab 08 — Dynamic inventory

**Concepts:** inventory plugins, constructed groups from cloud tags, `--graph`.

```bash
# Static YAML (this repo default)
ansible-inventory -i inventories/lab/hosts.yml --graph

# AWS EC2 plugin (needs AWS credentials)
# ansible-inventory -i inventories/prod/aws_ec2.yml --graph
```

Tag EC2 instances with `Role=web` and `Environment=prod` so `keyed_groups` creates `role_web` and `env_prod`. That is how you target cloud fleets without editing `hosts.yml`.
