# Lab 03 — Variables, facts, and Vault

**Concepts:** extra vars, group_vars, host_vars, facts, ansible-vault, precedence.

Precedence (high wins): extra vars (`-e`) > task vars > block vars > play vars > host_vars > group_vars > role defaults.

```bash
ansible-playbook labs/03-variables-facts-vault/vars_demo.yml
ansible-playbook labs/03-variables-facts-vault/vars_demo.yml -e nginx_listen_port=9090

cp vault/secrets.yml.example vault/secrets.yml
ansible-vault encrypt vault/secrets.yml
ansible-playbook labs/03-variables-facts-vault/vault_demo.yml --ask-vault-pass
```
