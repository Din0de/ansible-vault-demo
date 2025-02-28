# **Overview**

This repository demonstrates how to securely manage sensitive data using Ansible Vault. 
It provides a practical example of encrypting secrets (such as API keys, database passwords, 
and secret tokens) and referencing them in an Ansible playbook. This method enhances security 
by ensuring that critical information is not stored in plain text.

---

Repository Structure

ansible-vault-demo/
├── group_vars/
│   └── all/
│       ├── vault.yml       # Encrypted secrets (API key, DB password, secret token)
│       └── vars.yml        # Maps encrypted variables to simpler names for the playbook
├── inventory.ini           # Defines the host and connection details
└── playbook.yml            # Ansible playbook to decrypt and display the sensitive data

---

**Files and Their Purpose**

inventory.ini

Defines the inventory for the playbook. For this demo, it contains:
[local]
localhost ansible_connection=local

group_vars/all/vault.yml
An encrypted YAML file created using Ansible Vault. It contains sensitive variables:

vault_api_key: "super-secret-api-key"
vault_db_password: "database-password-123"
vault_secret_token: "secret-token-456"

group_vars/all/vars.yml
References the encrypted variables for use in the playbook:

api_key: "{{ vault_api_key }}"
db_password: "{{ vault_db_password }}"
secret_token: "{{ vault_secret_token }}"

playbook.yml
Contains the playbook that decrypts and displays the sensitive data using the debug module:

---
- hosts: local
  gather_facts: no

  tasks:
    - name: Display encrypted values (for demo only!)
      debug:
        msg:
          - "API Key: {{ api_key }}"
          - "DB Password: {{ db_password }}"
          - "Secret Token: {{ secret_token }}"

# **How to Use**

View or Edit the Vault File:
Use the following commands to view or edit the encrypted vault file:

ansible-vault view group_vars/all/vault.yml
ansible-vault edit group_vars/all/vault.yml

Run the Playbook:
To execute the playbook and display the decrypted values, run:

ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass

Prerequisites
Ansible: Version 2.9 or higher.
WSL/Ubuntu: The project is designed to run in a Windows Subsystem for Linux environment.
Git: For version control.
Python & Pip: Required for running Ansible.

