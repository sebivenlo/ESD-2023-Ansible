### Exercise: Configuring a Database

**Objective:**
Create an Ansible playbook that configures a database on target servers. Participants will need to identify and fix errors in variable assignments.

**[Broken Playbook Template](../Docker/ansible-playbooks/broken_configure_db.yml):**
```yaml
---
- name: Configure Database
  hosts: database_servers
  become: true

  vars:
    db_name: "my_database"
    db_user: "admin"
    db_password "admin_pass"

  tasks:
    - name: Create Database
      mysql_db:
        name: "{{ db_name }}"
        state: present

    - name: Create Database User
      mysql_user:
        name: "{{ db_user }}"
        password: "{{ db_password }}"
        priv: "{{ db_name }}.*:ALL"
        state: present
```

**Instructions for Participants:**
1. Review the provided `broken_configure_db.yml` playbook.
2. Identify and fix the intentional errors in variable assignments.
3. Run the corrected playbook against your target database servers.
   ```bash
   ansible-playbook -i inventory.ini fixed_configure_db.yml
   ```
4. Verify that the database and database user are configured as expected.

**Discussion Points:**
- How are variables used in Ansible playbooks?
- What are the common mistakes made in variable assignments in the provided playbook?
- How do the corrected variables affect the configuration of the database?

**Common Errors:**
1. Missing colon (`:`) in variable assignments.
2. Missing `=` in variable assignments.
3. Missing quotes around variable values.

Encourage participants to work through the exercise collaboratively, discuss their findings, and share their solutions. This exercise is designed to provide hands-on experience in fixing common Ansible playbook errors related to variables.


