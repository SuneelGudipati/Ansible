Here is the Ansible on Amazon Linux guide in English:

---

# Ansible on Amazon Linux

Ansible is a popular open-source automation tool used for configuration management, application deployment, and task automation. Running Ansible on Amazon Linux is efficient, especially for managing AWS infrastructure, as it integrates seamlessly with AWS services.

## Key Points for Using Ansible on Amazon Linux:

### 1. Installing Ansible on Amazon Linux

- **Update the system**:
   ```bash
   sudo yum update -y
   ```

- **Install EPEL Repository**:
   ```bash
   sudo amazon-linux-extras install epel -y
   ```

- **Install Ansible**:
   ```bash
   sudo yum install ansible -y
   ```

### 2. Configuring Ansible on Amazon Linux

- **Ansible Inventory**: Modify the inventory file:
   ```bash
   sudo nano /etc/ansible/hosts
   ```

- **SSH Access**: Ensure password-less SSH access is configured for the managed nodes.

### 3. Running Playbooks

- **Create Playbooks**:
   ```yaml
   ---
   - hosts: webservers
     tasks:
       - name: Install Nginx
         yum:
           name: nginx
           state: present
   ```

- **Execute Playbooks**:
   ```bash
   ansible-playbook playbook.yml
   ```

### 4. Managing AWS Resources

- **Install Python libraries for AWS modules**:
   ```bash
   pip install boto3 botocore
   ```

- **Set AWS credentials**:
   ```bash
   aws configure
   ```

### 5. Best Practices

- Use **roles** to organize playbooks.
- Define **variables** in separate files for flexibility.
- Use **version control** with Git to track changes.

### 6. Troubleshooting

- Use the `-v` flag for verbose output during playbook execution:
   ```bash
   ansible-playbook playbook.yml -v
   ```

- Ensure that SSH access is working and the nodes have proper sudo permissions.

---

This guide provides a concise explanation of how to set up, configure, and troubleshoot Ansible on Amazon Linux.
