Title: Debian SFTP User
Lead: Create and SFTP-only user in Debian Linux
Published: 23/Aug/20224
Tags:
  - Linux
  - Debian
  - sftp
  - ssh
---

# Create the user and folder structure
```bash
#add user without shell access
sudo adduser --shell /bin/false sftpuser 

#create the folder structure for the sftp
sudo mkdir -p /var/sftp/files 

#make the folder where the files are going to go and set initial permissions
sudo chown root:root /var/sftp
sudo chmod 755 /var/sftp 

#change permissiosn for just the 'file' section
sudo chown sftpuser:sftpuser /var/sftp/files 
```
# Configure SSH to limit what the user can do
```bash
#configure the sshd
sudo nano /etc/ssh/sshd_config
```

Add the following at the end of the file:
```
Match User sftpuser
	ForceCommand internal-sftp
	PasswordAuthentication yes
	ChrootDirectory /var/sftp
	PermitTunnel no
	AllowAgentForwarding no
	AllowTcpForwarding no
	X11Forwarding no
```

```bash
#restart the service
sudo systemctl restart ssh 
```
