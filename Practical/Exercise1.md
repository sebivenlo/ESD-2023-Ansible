### Exercise: Basic Web Server Deployment

**Objective:** Deploy an Ansible playbook with a static HTML page.

**[Playbook Template](../Docker/ansible-playbooks/deploy_web_server.yml):**

```yaml
---
- name: Install Nginx
  hosts: localhost
  become: yes  # Run tasks with sudo (root) privileges

  tasks:
    - name: Update package cache
      apt:
        update_cache: yes
      when: ansible_os_family == "Debian"  # Conditional task execution based on the OS family

    - name: Install Nginx
      apt:
        name: nginx
        state: present  # Ensure that the package is installed

    - name: Start Nginx service
      service:
        name: nginx
        state: started  # Ensure that the service is running

    - name: Enable Nginx service on boot
      service:
        name: nginx
        enabled: yes  # Ensure that the service starts on boot

```
**Instructions for Participants:**

1. Start the docker container with `docker-compose up -d`

2. Access the containers shell with `docker exec -it ansible-container /bin/bash`

3. Run the Ansible playbook against localhost with `ansible-playbook deploy_web_server.yml`. 
    
4. Verify that Nginx is installed and a basic HTML page is deployed, by opening localhost in your webbrowser.

5. Close the containers shell with STRG-D.