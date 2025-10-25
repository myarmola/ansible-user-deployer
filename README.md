# Ansible user deployer

This tool automates the process of managing Linux users: creating users and configuring SSH access. Ansible is used in cooperation with GitHub Actions, which allows scripts to be run automatically when new servers or users are added to the files.

## How it works

1) Each YAML file in the `users` folder contains user data, including name, groups and SSH key.
   
2) File `inventory.ini` contains all servers where users will be deployed.

3) Ansible adds the SSH keys for users to log in without a password.

4) It also allows users to execute sudo commands without prompting for a password.

## Prerequisites

On all servers, a user named `ansible` must be created with sudo privileges and the ability to execute sudo without a password.

A public key must also be added to `/home/ansible/.ssh/authorized_keys` from the `ANSIBLE_SSH_PRIVATE_KEY` variable.

## How to use

Adding a new user:

1) Create a new YAML file in the `users` folder. This file must contain the user's name, group, and SSH key. Example:

```yaml
# File: users/user.yaml
name: user
groups: sudo
ssh_key: ssh-rsa AAAAB3Nza...user@local
```

2) Commit to the `master` branch or create a pull request and merge into master. Changes to the repository automatically trigger the GitHub Actions workflow `users_deploying.yml`. Workflow executes a playbook that creates users on servers.
   
3) Wait until the workflow is successfully completed. Once completed, users can connect to servers with their SSH key.
