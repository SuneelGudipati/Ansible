Here is the GitHub-ready code for launching instances, installing Ansible on Amazon Linux, configuring passwordless SSH authentication, and running ad-hoc commands using Ansible, along with the setup of a sample playbook.

### **1. Launch Instances for Control Node and Managed Nodes (Amazon Linux)**

You can launch instances using AWS Management Console, AWS CLI, or Terraform. Ensure you have SSH access and assign a security group allowing SSH (port 22) for Control and Managed Nodes.

### **2. Install Ansible on the Control Node**

On your **Control Node** (Amazon Linux), execute the following commands:

```bash
# Update the system
sudo yum update -y

# Install EPEL Repository
sudo amazon-linux-extras install epel -y

# Install Ansible
sudo yum install ansible -y
```

### **3. Create a User on All Servers (Control and Managed Nodes)**

1. Create the user `ansibleuser` on the Control and Managed Nodes:

```bash
# Create the user
sudo useradd ansibleuser
sudo passwd ansibleuser
```

2. Grant sudo privileges to the `ansibleuser`:

```bash
sudo visudo
```

Add the following line under the `## Allow root to run any commands anywhere` section:

```bash
ansibleuser ALL=(ALL) NOPASSWD: ALL
```

### **4. Setup Passwordless Authentication**

#### On all the Servers:

1. Enable password authentication by editing the SSH config:

```bash
sudo vim /etc/ssh/sshd_config
```

   Set `PasswordAuthentication` to `yes`, then restart the SSH service:

```bash
sudo systemctl restart sshd
```

2. Generate an SSH key on the Control Node after login as ansibleuser:

```bash
sudo su ansibleuser
```

```bash
ssh-keygen -t rsa
```

3. Copy the SSH key to each Managed Node:

```bash
ssh-copy-id ansibleuser@<managed_node_ip>
```

4. Test the SSH connection:

```bash
ssh ansibleuser@<managed_node_ip>
```

### **5. Configure Ansible Hosts and Inventory**

1. Uncomment the inventory entry in the Ansible configuration file:

```bash
sudo vim /etc/ansible/ansible.cfg
```

2. Uncomment the following line:

```bash
inventory = /etc/ansible/hosts
```

3. Edit the Ansible hosts file:

```bash
sudo vim /etc/ansible/hosts
```

4. Add your managed nodes under groups like:

```ini
[web-servers]
managed_node1_ip
managed_node2_ip

[db-servers]
managed_node3_ip
managed_node4_ip
```

### **6. Run Ansible Ad-hoc Commands**

To test the connection with the Managed Nodes:

```bash
ansible all -m ping
```
Note: Add `interpreter_python=auto_silent` in the `/etc/ansible/ansible.cnf` file (anywhere).

Additional ad-hoc commands:

- **List all hosts:**

```bash
ansible all --list-hosts
```

- **Run `uptime` command:**

```bash
ansible all -m command -a "uptime"
```

- **Install `httpd` on all Managed Nodes:**

```bash
ansible all -m yum -a "name=httpd state=installed" -b
```

- **Start the `httpd` service:**

```bash
ansible all -m service -a "name=httpd state=started enabled=true" -b
```

- **Copy a file (e.g., `index.html`) to the Managed Nodes:**

```bash
ansible all -m copy -a "src=index.html dest=/var/www/html/" -b
```

### **7. Writing an Ansible Playbook**

Create an Ansible playbook to automate the installation and configuration of `httpd`:

```yaml
---
- name: Install and configure httpd on web servers
  hosts: web-servers
  become: yes

  tasks:
    - name: Install httpd
      yum:
        name: httpd
        state: present

    - name: Start and enable httpd service
      service:
        name: httpd
        state: started
        enabled: true
```

Save this playbook as `httpd_setup.yaml` and run it with:

```bash
ansible-playbook httpd_setup.yaml
```

### **8. Useful Ansible Playbook Commands**

- **Check syntax errors:**

```bash
ansible-playbook httpd_setup.yaml --syntax-check
```

- **Dry run (check mode):**

```bash
ansible-playbook httpd_setup.yaml --check
```
