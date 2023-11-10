### Exercise: Basic Web Server Deployment

**Objective:** Create an Ansible playbook to install and configure a basic web server (e.g., Nginx) and deploy a static HTML page.

**Playbook Template:**

```yaml
---
- name: Basic Web Server Deployment
  hosts: web_servers
  become: true  # Run tasks with sudo

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present  # Ensure Nginx is installed

    - name: Deploy HTML Page
      copy:
        content: "<html><body><h1>Hello, Ansible!</h1></body></html>"
        dest: "/var/www/html/index.html"

```
**Instructions for Participants:**

1. Set up a group of target servers in your inventory file (`inventory.ini`).
2. Run the Ansible playbook against your target servers.
    
    bash
    

1. `ansible-playbook -i inventory.ini deploy_web_server.yml`
    
2. Verify that Nginx is installed and a basic HTML page is deployed on the target servers.

**Discussion Points:**

- What is the purpose of the `hosts` directive in the playbook?
- How are tasks used to define the steps in the playbook?
- How does the `become: true` directive work, and why is it necessary in this playbook?
- What is the purpose of the `copy` module, and how is it used to deploy the HTML page?

This exercise is designed to introduce participants to basic Ansible playbook structure, tasks, and modules. It provides a hands-on experience with a simple scenario, allowing participants to run the playbook and observe the results on their target servers. Participants can then discuss and explore how to extend or modify the playbook for more complex scenarios.

### Exercise: Configuring a Database

**Objective:**
Create an Ansible playbook that configures a database on target servers. Participants will need to identify and fix errors in variable assignments.

**Broken Playbook Template (broken_configure_db.yml):**
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

### Exercise: Configuring Users with Ansible

**Objective:**
Create an Ansible playbook that configures user accounts on target servers based on variables, and includes conditionals and loops.

**Broken Playbook Template (broken_deploy_users.yml):**
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