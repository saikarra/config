# Ubuntu


## Base Install
```bash
apt update
apt upgrade -y
reboot now
apt autoclean

apt install -y htop curl wget vim sudo git
```

## Sai
```
# Create Backup User
adduser --disabled-password --gecos "Sai,,,," sai
bash -c 'echo "sai ALL=(ALL) NOPASSWD: ALL" | (EDITOR="tee -a" visudo)'

# SSH Key - Root
mkdir ~/.ssh
tee ~/.ssh/authorized_keys <<-'EOF'
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMeoAWg+XR8jt4uAa21i/lmlRcPvngVj3dllUYWqXBsC sai@saikarra.com
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAID1TnfsNHCMU2I8S56ZRbdMI04UNdEAr6Skzl9LRPZlk srkarra@us.ibm.com
EOF
chmod 750 ~/.ssh
chmod 640 ~/.ssh/authorized_keys
chown root:root -R ~/.ssh

# SSH Key - Sai
mkdir /home/sai/.ssh
tee /home/sai/.ssh/authorized_keys <<-'EOF'
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMeoAWg+XR8jt4uAa21i/lmlRcPvngVj3dllUYWqXBsC sai@saikarra.com
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAID1TnfsNHCMU2I8S56ZRbdMI04UNdEAr6Skzl9LRPZlk srkarra@us.ibm.com
EOF
chmod 750 /home/sai/.ssh
chmod 640 /home/sai/.ssh/authorized_keys
chown sai:sai -R /home/sai/.ssh

# SSH Keys
ssh-keygen -q -t ed25519 -C "sai@saikarra.com" -N '' -f ~/.ssh/id_ed25519
git config --global init.defaultBranch main
git config --global user.email "sai@saikarra.com"
git config --global user.name "Sai Karra"
```

## SSH Lockdown
```bash
sudo grep -q "^[^#]*PasswordAuthentication" /etc/ssh/sshd_config && sed -i "/^[^#]*PasswordAuthentication[[:space:]]yes/c\PasswordAuthentication no" /etc/ssh/sshd_config || echo "PasswordAuthentication no" >> /etc/ssh/sshd_config
systemctl restart sshd.service
reboot now
```



## Brian
```bash
# Create User
adduser --disabled-password --gecos "Pew Pew,,,," pewpew
bash -c 'echo "pewpew ALL=(ALL) NOPASSWD: ALL" | (EDITOR="tee -a" visudo)'

# SSH Key - Pew Pew
mkdir /home/pewpew/.ssh
tee /home/pewpew/.ssh/authorized_keys <<-'EOF'
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMeoAWg+XR8jt4uAa21i/lmlRcPvngVj3dllUYWqXBsC sai@saikarra.com
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAID1TnfsNHCMU2I8S56ZRbdMI04UNdEAr6Skzl9LRPZlk srkarra@us.ibm.com
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCtRqSgbit9iTTninEVp3hxbw6A8nDFQ+PTPMq/CiLmbfgFL5dAKMT+ny5I0rSuklO/+JX7JyQRMHvKu3SgSIWxtKWqvY9iwna4cmDh8qHPMYg8/8nURtDzPugnvArms58hb4USOz5zthU4E1vEvIWYy19bNtivKOYPGPHX+8/HBwyIdQDfcZffEMgdhHfClJicf+ew61CwLcimroNA1D+6/kRTBEJDg4G68YPKuCPBCrZlhLRrX1hRcstrmn4GThYrn63iMRtsRiiv8jt3lIcK8zuyjA+jNssUQn+OOrbK2Y/vh2cM1esBJ03GBbZ/ENvEHaGFbK1yWhWFEcQun5gal605XssoY7k1NtUPciV0nBT1n4rA+Od3tU4sVanOWDGWt92A1b4m43W5b8y883CcD2qbCxUBySS9skHEa04DBQWkSrWlLldfwuk2Uaxbig+r/C/EUGUz48g1Vtd+Jn2xWQEYo2TtUPWJ4ZSFhFyZySPazlwwx97ojIlSsldhfBs= briantsao@Brian's-MacBook-Pro
EOF

# Update Permissions
chmod 750 /home/pewpew/.ssh
chmod 640 /home/pewpew/.ssh/authorized_keys
chown pewpew:pewpew -R /home/pewpew/.ssh
```
