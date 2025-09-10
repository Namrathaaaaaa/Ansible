# Create AWS Resources with Ansible

## Overview
Use Ansible modules to automate AWS resource creation (EC2, S3, VPC, etc.) via API calls. Requires AWS credentials and boto3 library.

## Prerequisites
- AWS account & access keys
- Install `boto3` and `botocore` (Python)
- IAM user with permissions

## Example Playbook
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

## Run Playbook
```bash
ansible-playbook aws-ec2.yml
```

## Other AWS Modules
- `amazon.aws.s3_bucket` (S3)
- `amazon.aws.ec2_vpc` (VPC)
- `amazon.aws.rds_instance` (RDS)

---
**Tip:** Store credentials securely (env vars, vault).
