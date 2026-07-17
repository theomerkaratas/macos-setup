# Zsh Role

This Ansible role configures the Z shell (zsh) environment by deploying a customized `.zshrc` configuration file on macOS systems.

## Description

The role uses Ansible's template module to deploy a `.zshrc` configuration file from a Jinja2 template and reloads the shell configuration. The template includes conda initialization, shell aliases for common tools (git, docker, kubernetes, jupyter), and custom prompt configuration.

## Features

- Conda environment initialization
- Custom shell aliases for:
  - Git shortcuts
  - Docker container commands
  - API request shortcuts (curl-based kubectl alternatives)
  - Jupyter notebook activation
- Custom prompt configuration
- Automatic shell reload after configuration deployment

## Requirements

- Zsh installed on the target macOS system
- Ansible on the control machine

## Files

- `tasks/main.yml` - Role tasks that deploy the template and reload zsh
- `templates/.zshrc.j2` - Jinja2 template for the zsh configuration file

## Usage

Include this role in your playbook:

```yaml
- hosts: localhost
  roles:
    - zsh
```

## Customization

To customize the zsh configuration, edit the `templates/.zshrc.j2` file with your preferred aliases, environment variables, and shell settings. You can use Jinja2 templating variables to make configurations dynamic based on Ansible variables.
