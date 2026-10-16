# Lab 01 — Ad-hoc commands and inventory

**Concepts:** inventory, groups, patterns, ad-hoc vs playbooks.

```bash
# Graph of groups and hosts
ansible-inventory -i inventories/lab/hosts.yml --graph
ansible-inventory -i inventories/lab/hosts.yml --list

# Ad-hoc (one-off modules, no playbook file)
ansible all -m ansible.builtin.ping
ansible web -m ansible.builtin.command -a "hostname" --check
ansible 'web:&docker' -m ansible.builtin.debug -a "msg='intersection pattern'"
```

Job interview prompt: *When do you use ad-hoc vs a playbook?* Ad-hoc for one-off facts/restarts; playbooks for repeatable, reviewed change.
