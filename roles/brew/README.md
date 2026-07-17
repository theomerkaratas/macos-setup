# Brew Role

This Ansible role installs and manages Homebrew packages and GUI applications on macOS.

## Description

The role uses the `community.general.homebrew` and `community.general.homebrew_cask` modules to install Homebrew formulae (command-line tools) and casks (GUI applications) on macOS systems.

## Variables

### `homebrew_formulae`
List of Homebrew formulae (command-line tools) to install. Includes development tools, CLI utilities, DevOps tools, databases, and system utilities.

Default packages include: git, node, python@3.13, python@3.14, go, docker, kubernetes-cli, terraform, helm, and many more.

### `homebrew_casks`
List of Homebrew casks (GUI applications) to install. Includes development tools, container management, and utility applications.

Default casks include: chromium, docker, postman, vagrant, kubenav, and others.

## Requirements

- Homebrew installed on the target macOS system
- `community.general` Ansible collection

## Usage

Include this role in your playbook:

```yaml
- hosts: localhost
  roles:
    - brew
```

To customize the packages to install, override the variables in your playbook or inventory.
