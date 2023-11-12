### Exercise: Configuring Users with Ansible

**Objective:**
Create an Ansible playbook that configures user accounts on target servers based on variables, and includes conditionals and loops.

**[Broken Playbook Template](../Docker/ansible-playbooks/broken_deploy_users.yml):**
```yaml
---
- name: Configure Users
  hosts: target_servers
  become: true

  vars:
    users:
      - name: alice
        state: present
        groups: developers
      - name: bob
        state: present
        groups: administrators

  tasks:
    - name: Create or remove users
      user:
        name: "{{ item.name }}"
        state: "{{ item.state }}"
        groups: "{{ item.groups }}"
      with_items: "{{ users }}"
```

**Instructions for Participants:**
1. Review the provided `broken_deploy_users.yml` playbook.
2. Identify and fix the intentional errors in the playbook.
3. Run the corrected playbook against your target servers.
   ```bash
   ansible-playbook -i inventory.ini fixed_deploy_users.yml
   ```
4. Verify that user accounts are configured as expected on the target servers.

**Discussion Points:**
- How are variables used to define user configurations in Ansible?
- What is the purpose of the `with_items` directive, and how does it relate to loops?
- How are conditionals used in Ansible playbooks, and where do you find them in this exercise?

**Common Errors:**
1. Incorrect indentation
2. Typos in variable names
3. Missing quotes around variable values
4. Incorrect use of `with_items`

Encourage participants to collaborate, discuss their findings, and troubleshoot the playbook together. This exercise provides hands-on experience in fixing common Ansible playbook errors while reinforcing the concepts of variables, conditionals, and loops.
