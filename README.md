# **Ansible Vault Demo**


This repository demonstrates how to securely manage sensitive data using Ansible Vault. 
It was created to show how to encrypt secrets—such as API keys, database passwords, 
and tokens—and reference them in an Ansible playbook. The repository is intended for 
users who want to integrate secure secret management into their infrastructure-as-code workflows.

**Key components of the repository include:**

Inventory File: Defines hosts and connection details. 
For example, the file specifies a local host with the following content:
[local]
localhost ansible_connection=local

Encrypted Vault File: Located in group_vars/all/vault.yml, this file contains sensitive variables (e.g., API key, database password, and secret token) and is protected by a vault password.

Variables File: Found at group_vars/all/vars.yml, this file maps the encrypted variable names to simpler ones for easier reference in the playbook.

Playbook: The playbook.yml file runs against the local host group and uses the debug module to display decrypted values.

To use this project, ensure that you have installed Ansible, Python, and Git. 

The repository was set up in a Windows Subsystem for Linux (WSL) environment, 
making it a practical resource for users in similar setups. 
When you run the playbook with the command ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass, 
you will be prompted to enter the vault password. 

This process decrypts the sensitive data at runtime and allows the playbook to display the values securely.

**The benefits of using Ansible Vault, as demonstrated in this project, include:**

Preventing sensitive data from being stored in plain text.
Ensuring that credentials and secrets remain protected, even when code is shared or pushed to version control.
Streamlining the integration of security into your infrastructure management workflow.
