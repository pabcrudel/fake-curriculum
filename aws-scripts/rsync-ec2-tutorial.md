# How to deploy a website on AWS EC2 instance

## Install Apache on Amazon linux 2 AMI

```sh
sudo yum update -y
sudo yum install httpd -y
```

## Configure Apache

Newly AMI versions.

```sh
sudo service httpd start
sudo chkconfig httpd on
```

In older versions.

```sh
sudo systemctl start httpd
sudo systemctl enable httpd
```

## Install Rsync

Unix/Linux

```sh
sudo apt-get install rsync
```

Red Hat

```sh
sudo yum install rsync
```

## Rsync command

- The IP is fake

```sh
rsync -av -e "ssh -i labsuser.pem" website/ ec2-user@3.36.18.13:/var/www/html/
```
