# Create AWS Resources with Ansible

## Overview

Ansible can automate AWS resource creation (EC2, S3, VPC, etc.) using modules that interact with AWS APIs. You write playbooks to define what resources you want, and Ansible provisions them for you.

## Prerequisites

- AWS account & access keys
- Install `boto3` and `botocore` (Python)
- IAM user with permissions
- Add AWS credentials to environment, vault, or playbook

## Example 1: Launch EC2 Instance

```yaml
---
- name: Launch EC2 Instance
  hosts: localhost
  gather_facts: no
  tasks:
    - name: Create EC2
      amazon.aws.ec2_instance:
        key_name: mykey
        instance_type: t2.micro
        image_id: ami-12345678
        region: us-east-1
        count: 1
        aws_access_key: YOUR_KEY
        aws_secret_key: YOUR_SECRET
```

Run with:

```bash
ansible-playbook aws-ec2.yml
```

## Example 2: Create S3 Bucket

```yaml
---
- name: Create S3 Bucket
  hosts: localhost
  gather_facts: no
  tasks:
    - name: Create bucket
      amazon.aws.s3_bucket:
        name: my-ansible-bucket
        state: present
        region: us-east-1
        aws_access_key: YOUR_KEY
        aws_secret_key: YOUR_SECRET
```

Run with:

```bash
ansible-playbook aws-s3.yml
```

## Other AWS Modules

- `amazon.aws.ec2_vpc` (VPC)
- `amazon.aws.rds_instance` (RDS)
- `amazon.aws.s3_bucket` (S3)

---

**Tip:** Store credentials securely (env vars, vault). Use `hosts: localhost` for cloud provisioning.
