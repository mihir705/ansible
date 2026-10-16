# Lab 02 — Playbooks and modules

**Concepts:** play, task, module, FQCN, idempotency, check mode.

```bash
ansible-playbook playbooks/ping.yml --check
ansible-playbook playbooks/facts.yml
ansible-playbook labs/02-playbooks-and-modules/hello.yml
```

Idempotency: run twice; the second run should report `ok` / `changed=0` for modules that already match desired state.
