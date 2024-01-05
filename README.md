# Jenkins-master-slave

## Launch EC2 instance

To launch two EC2 ubuntu22 instance - one is master, another one is slave.

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/131849a8-96a2-4b4c-9483-003779e28283)

## Install java in both master and slave

```
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install openjdk-11-jre
java -version
```

## Install Jenkins on master node

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl status jenkins.service
```

## Access Jenkins console

http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 

1. Delete the inbound traffic rule for your instance
2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

<img width="1291" alt="215959008-3ebca431-1f14-4d81-9f12-6bb232bfbee3" src="https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/7921076d-377a-4ccd-bf63-d4b1c1a320f0">

### Click on Install suggested plugin

<img width="1291" alt="215959294-047eadef-7e64-4795-bd3b-b1efb0375988" src="https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/c2bc3fa6-d998-46e2-adce-0da35e055fb6">

Wait for the Jenkins to Install suggested plugins

<img width="1291" alt="215959398-344b5721-28ec-47a5-8908-b698e435608d" src="https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/d3153b98-d296-43c5-af43-465a86795cc1">

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

<img width="990" alt="215959757-403246c8-e739-4103-9265-6bdab418013e" src="https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/c72a064f-4bad-40f1-87c6-60028848b230">

## Add a new slave node to Jenkins master node

Jenkins - Manage Jenkins - Nodes - New node

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/7e3484f8-befc-434a-8414-c7237dc65e9f)

Jenkins Installation is Successful. You can now starting using the Jenkins

<img width="990" alt="215961440-3f13f82b-61a2-4117-88bc-0da265a67fa7" src="https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/ef0e59af-6ae4-4433-b081-4f1049aa1ce0">

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/cdf228fe-ae19-4fb3-a36e-2ad94762bdcb)

SSH to Jenkins slave node and create a new directory

```
sudo mkdir /opt/jenkins
sudo chmod 755 /opt/jenkins -R
```

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/fcd0f758-16c9-4678-ab57-29585f48b626)

### Create SSH Keygen in slave node

SSH to slave machine and perform below commands

```
ssh-keygen
```

copy a id_rsa (privatekey) for adding username with key in Jenkins credentials

copy a id_rsa.pub (publickey) and paste in below location of same slave node

```
sudo nano .ssh/authorized_keys
copy/paste the id_rsa.pub key here
save and exit
```

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/246e17ac-69ce-46af-ab62-583ec7413cd1)

### Jenkins console

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/3ccd35eb-0633-4b26-90c1-bf77812cfdbf)

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/9e7d8564-1491-46b3-ae7d-16a8f4eb98ee)

Enter username - ubuntu
Enter privatekey directly

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/87180aa9-e0a3-4f0d-a8f0-c5a418c23ffc)

![image](https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/d6f1cc77-f4db-42e0-a129-58bf6a846838)

Then save it.
