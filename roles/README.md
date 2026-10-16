# Roles

Reusable units (Terraform `modules/` equivalent).

| Role | What it configures |
|------|--------------------|
| `common` | timezone, baseline packages, motd template |
| `users` | Linux users from `desired_users` |
| `packages` | Extra packages from `role_packages` |
| `nginx` | Package, service, Jinja site + index, handler reload |
| `docker` | Engine install, group membership |
| `postgresql` | Server, database, user (password from vault) |
| `harden` | sshd PasswordAuthentication / PermitRootLogin |

Each role skips mutating tasks when `ansible_connection == local` so labs on a laptop stay safe. Point inventory at real SSH hosts to apply for real.
