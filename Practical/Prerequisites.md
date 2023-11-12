# Prerequisites

The files needed for docker are located in the docker folder.

### Start the Docker Container:

Run the following command in the directory where your `docker-compose.yml` file is located:

```bash
docker-compose up -d
```

This will start the Docker container defined in your `docker-compose.yml` file.

### Attach to the Docker Container:

Once the container is running, you can attach to it using the following command:

```bash
docker exec -it ansible-container bash
```

This will open a bash shell inside the running container.

### Run Ansible Playbook:

Once you are inside the container, navigate to the `/ansible/playbooks` directory (the mounted volume) and run your Ansible playbook. For example:

```bash
cd /ansible/playbooks
ansible-playbook your_playbook.yml
```

Replace `your_playbook.yml` with the actual name of your Ansible playbook.

### Verify the Ansible Execution:

After running the playbook, you should see the output of Ansible commands within the container.

Remember that any changes made inside the container will not persist after the container is stopped. If you need to keep the changes or want to inspect the container after the playbook run, you can do so before stopping the container.

### Stop the Docker Container:

When you are done, you can stop the Docker container:

```bash
docker-compose down
```

You can access Windows files from WSL by navigating to the /mnt directory, which is a mount point for the Windows file system.
