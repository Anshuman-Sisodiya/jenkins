### Steps to Install Jenkins on a t2.micro
```sudo apt update
sudo apt upgrade -y
```

### Create a 2GB swap file
```
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo /swapfile none swap sw 0 0 | sudo tee -a /etc/fstab
```

### Set swappiness to 90 for aggressive swap
As t2.micro only comes with 1GB RAM, we have to add swap-memory for jenkins to work properly

```
sudo sysctl vm.swapniess=90
echo vm.swappiness=90 | sudo tee -a /etc/sysctl.conf
```

### Install Java
```
sudo apt install openjdk-21-jdk
java --version
```

### Install Jenkins
```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
