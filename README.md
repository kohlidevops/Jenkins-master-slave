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

Jenkins Installation is Successful. You can now starting using the Jenkins

<img width="990" alt="215961440-3f13f82b-61a2-4117-88bc-0da265a67fa7" src="https://github.com/kohlidevops/Jenkins-master-slave/assets/100069489/ef0e59af-6ae4-4433-b081-4f1049aa1ce0">

