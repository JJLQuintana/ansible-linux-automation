# Ansible Linux Automation

Hands-on lab covering Ansible ad hoc commands and playbooks for managing remote Linux servers.

## What this covers
- Running elevated ad hoc commands (`--become --ask-become-pass`)
- Installing and updating packages with the `apt` module (`vim-nox`, `snapd`)
- Writing a playbook that installs Apache2 and PHP support
- Reading playbook output (`ok`, `changed`, `failed`, `unreachable`)

## Lab environment
- Control node: Ubuntu workstation running Ansible
- Managed nodes: Ubuntu server and a CentOS server (VirtualBox, host-only network)

## Repository contents
| File | Purpose |
|------|---------|
| `ansible.cfg` | Ansible configuration |
| `inventory` | Managed hosts |
| `playbook.yaml` | Initial trial playbook |
| `install_apache.yml` | Updates the package index, installs apache2, adds PHP support |

## Usage
```bash
ansible all -m apt -a update_cache=true --become --ask-become-pass
ansible-playbook --ask-become-pass install_apache.yml
```

## Key takeaways
- Ad hoc commands fail without privilege escalation; `--become` fixes that.
- `state=latest` ensures a package is current, while the default only ensures it is present.
- The playbook succeeded on the Ubuntu host but failed on CentOS, because the `apt` module doesn't work on RPM-based systems. A distro-aware playbook would use `dnf`/`yum` there, or the generic `package` module.
