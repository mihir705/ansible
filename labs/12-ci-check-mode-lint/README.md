# Lab 12 — Check mode, diff, and CI lint

**Concepts:** `--check`, `--diff`, `ansible-lint`, GitHub Actions.

```bash
ansible-playbook playbooks/ping.yml --check --diff
ansible-playbook labs/02-playbooks-and-modules/hello.yml --check --diff
ansible-lint
```

`--check` is the Ansible equivalent of `tofu plan` for many modules (not all cloud modules fully support it).
