# Ansible

## Ansible Commands

```text
| Command                                        | Description                                   |
| ---------------------------------------------- | --------------------------------------------- |
|   ansible --version                            | Displays the installed Ansible version.       |
|   ansible all -m ping                          | Tests connectivity to hosts in the inventory. |
|   ansible-inventory --list                     | Displays the complete inventory structure.    |
|   ansible all -m command -a "uptime"           | Executes a command on remote servers.         |
|   ansible-playbook playbook.yml                | Executes an Ansible playbook.                 |
|   ansible-playbook --check playbook.yml        | Performs a dry run without applying changes.  |
|   ansible-playbook --syntax-check playbook.yml | Validates playbook syntax.                    |

```
