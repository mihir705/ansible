# Lab 06 — Roles and Galaxy

**Concepts:** role layout (`tasks`, `handlers`, `defaults`, `templates`, `meta`), `ansible-galaxy`, collections vs roles.

```bash
ansible-galaxy collection list
ansible-playbook playbooks/web.yml --tags web --check
tree -L 3 roles/nginx
```

Interview prompt: *Role vs collection?* A role is reusable tasks/files. A collection packages modules, plugins, and roles (for example `amazon.aws`).
