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
