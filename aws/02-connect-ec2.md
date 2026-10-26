# Connect AWS EC2 Ubuntu instance using SSH key

## Go to your .ssh directory
```bash
cd .\.ssh\
```

## Create your ssh public and private key
```bash
cd .\.ssh\
ssh-keygen -t ed25519 -C "ec2-key" -f ".\ec2-key"
```

## Copy your public key
```bash
cat .\ec2-key.pub
```
# Add public key to EC2

## Create .ssh directory and set permissions
```bash
sudo install -d -m 700 -o ubuntu -g ubuntu /home/ubuntu/.ssh
```

## Add here your local machine public key
```bash
echo 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA... aws-ec2-key' | sudo tee -a /home/ubuntu/.ssh/authorized_keys > /dev/null
```

## Fixed Permissions
```bash
sudo chown ubuntu:ubuntu /home/ubuntu/.ssh/authorized_keys
sudo chmod 600 /home/ubuntu/.ssh/authorized_keys
```

## Verify your ssh key
```bash
sudo tail -n 3 /home/ubuntu/.ssh/authorized_keys
```

## Connect your ec2 instance
```bash
ssh -i ".\aws-ec2-key" ubuntu@YOUR_EC2_PUBLIC_IP
```