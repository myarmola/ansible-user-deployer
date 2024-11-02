# SSH user management

This repository automates the SSH user management process: creating users and setting up SSH access. For this, Ansible is used together with GitHub Actions, which allows you to run scripts automatically when changes are made to the repository.

## Functional capabilities

Automated user creation:

1) Each YAML file in the `users` folder contains user data, including name, groups, and SSH key.
   
2) File `inventory.ini` contains all servers where users will be deployed.

3) Configuring SSH Access: Adds SSH keys for users to login without a password.

4) Setting sudo privileges: Allows users to execute sudo commands without prompting for a password.

## How to use

Adding a new user:

1) Create a new YAML file in the **_users_** folder, the file name should match the user's name (for example, `example.user.yaml`).
The content of the file must contain the user's name, group, and SSH key. Example:

```yaml
# File: users/n.surname.yaml
name: n.surname
groups: sudo
ssh_key: ssh-rsa AAAAB3Nza...n.surname@example.local
```

2) Commit to the `master` branch or create a pull request and merge into master. Changes to the repository automatically trigger the GitHub Actions workflow `users_deploying.yml`. Workflow executes a playbook that creates users on servers.
   
4) Check the changes on server.
