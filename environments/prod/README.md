# prod environment

Same idea as `terraform-aws/environments/prod`: one place to run everything for an environment.

```bash
cd ../..
ansible-playbook -i inventories/prod/hosts.yml playbooks/site.yml --check
ansible-playbook -i inventories/prod/hosts.yml playbooks/site.yml --tags web
ansible-playbook -i inventories/prod/hosts.yml playbooks/site.yml --limit web1
```

Edit `inventories/prod/hosts.yml` with real SSH targets before applying.
