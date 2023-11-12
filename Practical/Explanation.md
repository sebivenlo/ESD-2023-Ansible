---
# Introduction to Ansible Playbooks

## What are Ansible Playbooks?

Ansible Playbooks are YAML files that define a set of tasks to be executed on remote hosts. They serve as a powerful tool for automating complex IT tasks, from configuration management to application deployment.

## Key Components:

1. **Hosts:**
   - Specifies the target machines where the playbook will be executed.

   ```yaml
   hosts: webservers
   ```

2. **Tasks:**
   - Describes a series of steps to be performed on the hosts.

   ```yaml
   tasks:
     - name: Ensure Apache is installed
       yum:
         name: httpd
         state: present
     - name: Start Apache service
       service:
         name: httpd
         state: started
   ```

3. **Handlers:**
   - Defines tasks to be run only if notified by other tasks.

   ```yaml
   handlers:
     - name: restart apache
       service:
         name: httpd
         state: restarted
   ```

## Playbook Execution:

- Ansible Playbooks are executed using the `ansible-playbook` command.
- They provide a structured and readable way to define and execute automation tasks.

## Example Playbook:

```yaml
---
- name: Configure Web Servers
  hosts: webservers
  become: true

  tasks:
    - name: Ensure Apache is installed
      yum:
        name: httpd
        state: present

    - name: Copy Apache configuration file
      copy:
        src: files/httpd.conf
        dest: /etc/httpd/conf/httpd.conf
      notify:
        - restart apache

  handlers:
    - name: restart apache
      service:
        name: httpd
        state: restarted
```

# Understanding Ansible Variables

## Introduction to Ansible Variables:

Ansible variables play a crucial role in customizing and controlling the behavior of Ansible playbooks. They allow you to define dynamic values that can be used throughout your playbooks, making them more flexible and adaptable to different environments.

## Types of Ansible Variables:

1. **Global Variables:**
   - Defined in the `group_vars` or `host_vars` directory.
   - Apply to all hosts or specific hosts respectively.

2. **Playbook Variables:**
   - Defined within a playbook using the `vars` keyword.
   - Scoped to a specific playbook.

3. **Facts:**
   - Automatically collected by Ansible about remote systems.
   - Accessed using the `ansible_facts` variable.

4. **Environment Variables:**
   - Set externally and accessed within Ansible playbooks.

## Variable Syntax:

- Ansible variables are enclosed in double curly braces, like `{{ variable_name }}`.
- You can also use the Jinja2 templating language for more advanced variable usage.

## Example:

```yaml
---
# Playbook with Variables
- name: Configure Web Servers
  hosts: webservers
  vars:
    http_port: 80
    max_clients: 200

  tasks:
    - name: Ensure Apache is installed
      yum:
        name: httpd
        state: present

    - name: Configure Apache
      template:
        src: /etc/httpd.conf.j2
        dest: /etc/httpd.conf
      notify:
        - restart apache
```

## Leveraging Ansible Loops and Conditionals

### Introduction to Loops and Conditionals

In Ansible, loops and conditionals are powerful constructs that enable automation engineers to iterate over tasks and apply logic based on specific conditions. These features enhance the flexibility and efficiency of Ansible playbooks.

### Loops in Ansible

**1. With_Items Loop:**
   - Iterates over a list of items.
   - Executes tasks for each item.

   ```yaml
   - name: Install required packages
     yum:
       name: "{{ item }}"
       state: present
     with_items:
       - httpd
       - mysql
       - php
   ```

**2. Looping over a Range:**
   - Iterates over a range of numbers.

   ```yaml
   - name: Create multiple users
     user:
       name: user{{ item }}
       state: present
     with_sequence: start=1 end=5
   ```

### Conditionals in Ansible

**1. When Statement:**
   - Executes a task based on a specified condition.

   ```yaml
   - name: Restart Apache if configuration file changes
     service:
       name: httpd
       state: restarted
     when: "'httpd.conf' in changed_files.stdout"
   ```

**2. Fail Module:**
   - Aborts the playbook if a condition is not met.

   ```yaml
   - name: Check if required software is installed
     fail:
       msg: "Required software is not installed."
     when: "'required_software' not in ansible_facts.packages"
   ```

### Combining Loops and Conditionals

```yaml
- name: Configure web servers
  hosts: webservers
  tasks:
    - name: Ensure required packages are installed
      yum:
        name: "{{ item }}"
        state: present
      with_items:
        - httpd
        - mysql
        - php

    - name: Configure Apache virtual hosts
      template:
        src: "{{ item.src }}"
        dest: "/etc/httpd/conf.d/{{ item.name }}"
      with_items:
        - { src: "templates/site1.j2", name: "site1.conf" }
        - { src: "templates/site2.j2", name: "site2.conf" }
      notify:
        - restart apache
```

In this example, the playbook installs packages and configures Apache virtual hosts using both loops and conditionals.
