### Commands

- aws ec2 describe-vpcs
- `vpc_id=$(aws ec2 describe-vpcs --query 'Vpcs[1].VpcId' --output text)` Retrieve the VPC ID
- `subnet_id=$(aws ec2 describe-subnets --filters "Name=vpc-id,Values=$vpc_id" | jq -r '.Subnets[].SubnetId' | head -n 1)` Retrieve the Subnet ID
- `sg_name="SgAwsCli"` Set the Security Group name
- `aws ec2 create-security-group --group-name $sg_name --description "My Security Group aws cli" --vpc-id $vpc_id`
- `sg_id=$(aws ec2 describe-security-groups --group-names $sg_name --query 'SecurityGroups[0].GroupId' --output text)`
- `aws ec2 authorize-security-group-ingress --group-id $sg_id --protocol tcp --port 80 --cidr 0.0.0.0/0`
- `aws ec2 authorize-security-group-ingress --group-id $sg_id --protocol tcp --port 22 --cidr 0.0.0.0/0`
- `ami=$(aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn2-ami-hvm-2.0.*-x86_64-gp2" --region us-east-1 --query 'reverse(sort_by(Images, &CreationDate))[0].ImageId' --output text)`
- `t2micro=$(aws ec2 describe-instance-types --filters "Name=instance-type,Values=t2.micro" --query 'InstanceTypes[].InstanceType' --output text)` Get the instance type
- kp="keypair"
- aws ec2 run-instances --image-id $ami --instance-type $t2micro --key-name $kp --security-group-ids $sg_id --subnet-id $subnet_id --region us-east-1
