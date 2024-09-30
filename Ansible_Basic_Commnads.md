# Essential Ansible Commands

This guide contains some essential Ansible commands with their explanations for managing infrastructure efficiently.

### 1. Ping all hosts to check connectivity
```bash
ansible all -m ping
```
This command checks the connection to all hosts in the inventory file.

### 2. Run a command on all hosts
```bash
ansible all -m shell -a "uptime"
```
This runs the `uptime` command on all hosts. You can replace `uptime` with any command you want to run.

### 3. Run a playbook
```bash
ansible-playbook playbook.yml
```
This runs the `playbook.yml` file against the hosts defined in the inventory.

### 4. Specify a different inventory file
```bash
ansible-playbook -i myinventory.ini playbook.yml
```
This uses `myinventory.ini` instead of the default `/etc/ansible/hosts`.

### 5. List hosts in the inventory
```bash
ansible all --list-hosts
```
This lists all the hosts in your inventory.

### 6. Use tags in a playbook
```bash
ansible-playbook playbook.yml --tags "mytag"
```
This runs only the tasks tagged with `mytag` in the `playbook.yml`.

### 7. Run playbook on specific host/group
```bash
ansible-playbook -l webservers playbook.yml
```
This runs the playbook only on hosts defined under the `webservers` group in the inventory.

### 8. Check syntax of playbook
```bash
ansible-playbook playbook.yml --syntax-check
```
This checks for any syntax errors in your `playbook.yml`.

### 9. Dry run (check mode)
```bash
ansible-playbook playbook.yml --check
```
This performs a dry run to see what changes would be made without actually applying them.

### 10. Show output in JSON format
```bash
ansible all -m shell -a "uptime" -o
```
This command shows the output in a JSON-like format.

### 11. Gather facts about hosts
```bash
ansible all -m setup
```
This gathers detailed information about all hosts, such as OS type, network interfaces, etc.

### 12. Execute a playbook with a specific user
```bash
ansible-playbook playbook.yml -u username
```
This runs the playbook as the specified user (`username`).

### 13. Run a playbook with sudo privileges
```bash
ansible-playbook playbook.yml --become
```
This runs the playbook with sudo privileges.

### 14. View available roles
```bash
ansible-galaxy list
```
This lists all installed roles in Ansible.

### 15. Install a role from Ansible Galaxy
```bash
ansible-galaxy install username.role_name
```
This installs a role from Ansible Galaxy. Replace `username` and `role_name` with the actual role name.

---

These are some of the most commonly used commands in Ansible to manage infrastructure efficiently.
```
