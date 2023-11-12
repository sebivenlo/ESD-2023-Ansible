### Exercise: Extending PostgreSQL Setup with Database and Table Creation

**Objective:** Enhance the existing Ansible playbook to include tasks for creating a PostgreSQL database and defining tables within it.

**Instructions:**

1. **Current Ansible Playbook:**
   ```yaml
   ---
- name: Install PostgreSQL and configure database
  hosts: localhost
  become: yes  # Run tasks with sudo (root) privileges

  vars:
    postgres_db_name: "your_database_name"
    postgres_user: "your_username"
    postgres_password: "your_password"

  tasks:
    - name: Install PostgreSQL and its dependencies
      apt:
        name: "{{ item }}"
        state: present
      with_items:
        - postgresql
        - postgresql-contrib

    - name: "Install Python packages"
      pip: "name={{ item }}  state=present"
      with_items:
        - psycopg2-binary

    - name: Start and enable PostgreSQL service
      service:
        name: postgresql
        state: started
        enabled: yes

    - name: Create PostgreSQL user
      postgresql_user:
        name: "{{ postgres_user }}"
        password: "{{ postgres_password }}"
        encrypted: yes
        state: present

    - name: Grant all privileges on the database to the user
      postgresql_privs:
        database: "{{ postgres_db_name }}"
        user: "{{ postgres_user }}"
        priv: ALL
        state: present

   ```

2. **Tasks to Extend the Playbook:**

   a. **Task 4: Create a PostgreSQL Database**
      - Add a task to create a new PostgreSQL database with a specified name.
      - Utilize the `postgresql_db` Ansible module for this task.

   b. **Task 5: Define Tables in the Database**
      - Extend the playbook to include tasks that define tables within the created database.
      - Use the `postgresql_table` Ansible module to define tables with specific columns.

3. **Hints:**
   - Refer to the Ansible documentation for the `postgresql_db` and `postgresql_table` modules.
   - Consider using variables for the database and table names to make the playbook more flexible.
   - Test the extended playbook on a local environment before applying it to production.

