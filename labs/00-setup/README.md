# Lab 00 — Setup

Install Ansible and collections used by this repo.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install 'ansible-core>=2.16' ansible-lint
ansible-galaxy collection install -r requirements.yml
ansible --version
ansible-inventory --graph
```

Expected: inventory graph shows `web`, `db`, `control`, `docker`.
