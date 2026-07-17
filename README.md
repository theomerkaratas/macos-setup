# macOS Setup

Automated macOS machine setup using Ansible. This project automates the installation and configuration of development tools, shell environments, and GUI applications on macOS.

## Overview

This Ansible playbook automates the setup of a fresh macOS machine with:
- **Homebrew formulae** - Command-line tools for development, DevOps, and system utilities
- **Homebrew casks** - GUI applications and tools
- **Zsh configuration** - Custom shell environment with aliases and settings

## Prerequisites

- macOS (10.14 or later)
- [Homebrew](https://brew.sh/) installed
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html) installed (can be installed via Homebrew: `brew install ansible`)
- Python 3 installed (can be installed via `brew install python@3.14`)
- Git installed (can be installed via `brew install git`)

## Installation & Usage

1. **Clone this repository:**
   ```bash
   git clone <repository-url>
   cd macos-setup
   ```

2. **Install Ansible community collection (if not already installed):**
   ```bash
   ansible-galaxy collection install community.general
   ```

3. **Run the playbook:**
   ```bash
   ansible-playbook playbook.yml
   ```

   Or with sudo for system-level operations:
   ```bash
   ansible-playbook playbook.yml -K
   ```

## Project Structure

```
macos-setup/
├── README.md              # This file
├── ansible.cfg            # Ansible configuration
├── playbook.yml           # Main playbook
├── roles/
│   ├── brew/              # Homebrew role
│   │   ├── README.md
│   │   ├── defaults/
│   │   │   └── main.yml   # Package lists
│   │   └── tasks/
│   │       └── main.yml   # Installation tasks
│   └── zsh/               # Zsh configuration role
│       ├── README.md
│       ├── tasks/
│       │   └── main.yml   # Configuration tasks
│       └── templates/
│           └── .zshrc.j2  # Zsh configuration template
```

## Roles

### Brew Role
Installs Homebrew packages including:
- **Core tools**: git, zsh, curl, wget, httpie
- **Development**: node, python, go, php, maven, docker
- **Kubernetes & Cloud**: kubernetes-cli, helm, minikube, k9s, krew, argocd
- **DevOps**: terraform, ansible, packer, vault, consul, prometheus, grafana
- **CLI utilities**: tmux, fzf, ripgrep, bat, fd, jq, yq, gh
- **Databases**: mysql, sqlite, libpq
- **GUI apps**: chromium, postman, docker, vagrant, drawio, and more

See [roles/brew/README.md](roles/brew/README.md) for details.

### Zsh Role
Configures the Z shell environment with:
- Conda initialization
- Custom shell aliases for git, docker, kubernetes, jupyter
- Custom prompt configuration
- Jinja2 template-based configuration for customization

See [roles/zsh/README.md](roles/zsh/README.md) for details.

## Customization

### Modify Package Lists

Edit the variable files to customize what gets installed:

- **Homebrew formulae**: Edit [roles/brew/defaults/main.yml](roles/brew/defaults/main.yml)
- **Homebrew casks**: Edit [roles/brew/defaults/main.yml](roles/brew/defaults/main.yml)
- **Zsh configuration**: Edit [roles/zsh/templates/.zshrc.j2](roles/zsh/templates/.zshrc.j2)

### Override Variables in Playbook

Add variable overrides to `playbook.yml`:

```yaml
---
- hosts: localhost
  connection: local
  vars:
    homebrew_formulae:
      - git
      - node
      # ... custom list
  roles:
    - brew
    - zsh
```

## Running Specific Roles

To run only the Homebrew role:
```bash
ansible-playbook playbook.yml --tags brew
```

To run only the Zsh configuration role:
```bash
ansible-playbook playbook.yml --tags zsh
```

## Troubleshooting

- **Homebrew not found**: Install Homebrew first from https://brew.sh/
- **Ansible not found**: Install with `brew install ansible`
- **Permission denied**: Some Homebrew operations may require sudo. Run with `-K` flag to prompt for password
- **Python version mismatch**: Check that Python 3 is being used in `ansible.cfg`

## Notes

- This playbook is idempotent - running it multiple times is safe and will only install missing packages
- The playbook targets `localhost` with local connection for convenience
- Existing packages are not reinstalled, only missing ones are installed
- Configuration changes (zsh) only trigger on template changes

## Resources

- [Ansible Documentation](https://docs.ansible.com/)
- [Homebrew Documentation](https://docs.brew.sh/)
- [Zsh Documentation](http://zsh.sourceforge.net/Doc/)

