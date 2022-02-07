# Set up SSH connection on Windows Server

## 1.create SSH key as usuall

## 2.open C:\ProgramData\ssh\sshd_config as an Administrator:
  notepad sshd_config

## 3.add new port:
  Port 1234
  
## 4.change the sshd_config file:<br />
  PermitRootLogin no <br />
  PubkeyAuthentication yes <br />
  PasswordAuthentication no <br />
  \#GSSAPIAuthentication no <br />
  \#Match Group administrators <br />
  \#   AuthorizedKeysFile __PROGRAMDATA__/ssh/administrators_authorized_keys

## 5.Allow the SSH port in Windows Firewall. By default, the server is using port 22. Run this command in an elevated command prompt:
  netsh advfirewall firewall add rule name="SSHD Port" dir=in action=allow protocol=TCP localport=22
  
## 6.Start the SSG service and/or configure automatic start:
  Go to Control Panel > System and Security > Administrative Tools and open Services. Locate OpenSSH SSH Server service.
  If you want the server to start automatically when your machine is started: Go to Action > Properties. In the Properties dialog, change Startup type to Automatic and confirm.
  Start the OpenSSH SSH Server service by clicking the Start the service.

## 7.Connect by the SSH client
  ssh -i path\to\id_rsa -p portnumber username@ip <br />
  e.g.: ssh -i .\id_rsa -p 1234 John@123.123.123.123
