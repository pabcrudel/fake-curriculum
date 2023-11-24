# How to deploy a website on AWS EC2 instance

## Step 1: Install Apache on Amazon linux 2 AMI

Update the package manager and install Apache on your Amazon Linux 2 instance.

- Note: It's being using `yum` because the Amazon linux 2 AMI uses it instead of
  `apt-get`.

```sh
sudo yum update -y
sudo yum install httpd -y
```

## Step 2: Configure Apache

For newly AMI versions, start Apache and configure it to launch on boot.

```sh
sudo service httpd start
sudo chkconfig httpd on
```

For older versions, use the following commands.

```sh
sudo systemctl start httpd
sudo systemctl enable httpd
```

## Step 3: Install Rsync

Install Rsync based on your operating system.

### For Unix/Linux

```sh
sudo apt-get install rsync
```

### For Red Hat

```sh
sudo yum install rsync
```

## Step 4: Rsync command

Use Rsync to transfer your website files to the EC2 instance.

- Download `labsuser.pem` from AWS Academy Lab.
- Change `website/` with your website folder o path.
- Change `3.36.18.13` with the IP of your EC2 Instance.

```sh
rsync -av -e "ssh -i labsuser.pem" website/ ec2-user@3.36.18.13:/var/www/html/
```
