### Commands

- aws ec2 describe-vpcs
- ´vpc_id=$(aws ec2 describe-vpcs --query 'Vpcs[1].VpcId' --output text)´ Retrieve the VPC ID
