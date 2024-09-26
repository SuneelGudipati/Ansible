# Ansible on Amazon Linux: Key Interview Points

## Overview
This repository outlines the essential concepts of using Ansible on Amazon Linux, designed to assist in interview preparation.

## Key Points

1. **What is Ansible?**
   - An open-source IT automation tool for configuration management, application deployment, and orchestration.
   - Uses YAML in Playbooks for writing automation scripts.

2. **Installing Ansible on Amazon Linux**
   - Install via the EPEL repository:
     ```bash
     amazon-linux-extras install epel
     ```
   - Install Ansible with:
     ```bash
     yum install ansible
     ```

3. **How Ansible Communicates with Managed Nodes**
   - **Agentless:** No software installation required on managed nodes.
   - Uses SSH for Linux and WinRM for Windows for communication.

4. **Configuring SSH on Amazon Linux for Ansible**
   - Set up passwordless SSH using SSH key pairs to enable task execution without manual input.

5. **Ansible Inventory**
   - Default location: `/etc/ansible/hosts`.
   - Lists managed machines and allows for grouping (e.g., webservers, databases).

6. **Using Ansible Playbooks on Amazon Linux**
   - YAML-based scripts defining tasks to manage local and remote nodes (e.g., package installation, service management).

7. **Ansible Modules for AWS**
   - Dedicated modules for managing AWS services (EC2, S3, RDS, IAM, VPC).
   - Requires Python packages like `boto3` and `botocore`.

8. **Handling AWS Credentials in Ansible**
   - Use the AWS CLI:
     ```bash
     aws configure
     ```
   - Alternatively, set environment variables:
     ```bash
     export AWS_ACCESS_KEY_ID=your_access_key
     export AWS_SECRET_ACCESS_KEY=your_secret_key
     ```

9. **Ansible Roles on Amazon Linux**
   - Reusable units for structuring Playbooks and organizing tasks, variables, and handlers.

10. **Using Ansible Vault**
    - Secures sensitive information (passwords, keys) by encrypting data in playbooks or variable files.

11. **Advantages of Using Ansible on Amazon Linux**
    - Optimized for AWS, enhancing integration with AWS services.
    - Agentless nature suits dynamic cloud environments.
    - Flexibility in scaling AWS resources automatically.

12. **Common Use Cases for Ansible on Amazon Linux**
    - Provisioning/configuring EC2 instances.
    - Automating application deployments and infrastructure changes.
    - Integrating with AWS services for cloud management.
    - Managing configurations across multiple AWS instances.

13. **Best Practices for Ansible on Amazon Linux**
    - Use version control (e.g., Git) for playbooks.
    - Modularize playbooks with roles for maintainability.
    - Utilize tags to run specific tasks.
    - Implement error handling with `ignore_errors` where necessary.
    - Use `ansible-lint` to check for best practices and syntax errors.
