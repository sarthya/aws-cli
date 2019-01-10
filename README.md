# docker + docker-compose + aws-cli + ecs-cli

## Ξ install docker in ubuntu box
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
## Ξ install docker-compose in ubuntu box

### 1. Run this command to download the latest version of Docker Compose:
```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
### 2. Apply executable permissions to the binary:
```
$ sudo chmod +x /usr/local/bin/docker-compose
```
## Ξ install AWS cli in ubuntu box
```
$ apt-get update && apt-get install awscli
```
## OR
### 1. Install latest python binary:
```
$ sudo apt-get install python3-pip
```
### 2. Install latest version of aws-cli:
```
$ pip3 install --upgrade awscli
```

## Ξ install ecs-cli in ubuntu box
### 1. Download the ECS CLI binary.
```
$ sudo curl -o /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest
```
### 2. Apply Execute Permissions to the Binary
```
$ sudo chmod +x /usr/local/bin/ecs-cli
```

### there are steps between 1 and 2 to verify the signature, which are not mentioned here..

## Ξ install java8 in ubuntu box
### 1. add ppa binary.
```
$ sudo add-apt-repository ppa:webupd8team/java
```
### 2. Update and install the installer script:
```
$ sudo apt update; sudo apt install oracle-java8-installer
```

### 3. Set Java environment variables
```
$ sudo apt install oracle-java8-set-default
```
### 4. find java path
```
$ type -p javac|xargs readlink -f|xargs dirname|xargs dirname
```

### 4. Set JAVA_HOME
```
$ export JAVA_HOME=<OUTPUT of step 3, abaove step>
```

### 4. Set PATH
```
$ export PATH=$PATH:$JAVA_HOME/bin
```

## Ξ install maven in ubuntu box
### 1. Install maven .
```
$ sudo apt-get install maven
```


















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
