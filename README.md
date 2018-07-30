# aws-cli
## install AWS cli in ubuntu box
```
apt-get update && apt-get install awscli
```
a collection of aws cli commands 
## Creating AWS instance with TAG name
#### $ sh run.sh <instance tag name>
```
#!/bin/bash
VAR=`aws ec2 run-instances --image-id ami-********** \
--subnet-id subnet-************* \
--security-group-ids sg-*********** \
--count 1 \
--instance-type t2.micro \
--key-name <something.pem file name as something> \
--region us-east-1 | grep InstanceId | cut -d ':' -f 2 | awk '{ gsub("\"",""); gsub(",",""); print $1 }'`
echo $VAR
EXEC=`aws ec2 create-tags --region us-east-1 --resources $VAR --tags Key=Name,Value=$1`
```
