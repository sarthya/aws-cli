# docker + docker-compose + aws-cli + ecs-cli

## install docker in ubuntu box
### 1. Update the apt package index.
```
$ sudo apt-get update
```
### 2. Install packages to allow apt to use a repository over HTTPS:
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```
### 3. Add Docker’s official GPG key:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
### 4. Add Docker’s official GPG key:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
#### Verify that you now have the key with the fingerprint
```
$ sudo apt-key fingerprint 0EBFCD88
```
### 5. Use the following command to set up the stable repository.
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
### 6. Update the apt package index.
```
$ sudo apt-get update
```
### 7. Install the latest version of Docker CE, or go to the next step to install a specific version:
```
$ sudo apt-get install docker-ce
```
## install docker-compose in ubuntu box

### 1. Run this command to download the latest version of Docker Compose:
```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
### 2. Apply executable permissions to the binary:
```
$ sudo chmod +x /usr/local/bin/docker-compose
```
## install AWS cli in ubuntu box
```
$ apt-get update && apt-get install awscli
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
