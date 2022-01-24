# Set up SSH connection on Windows Server

1.create SSH key as usuall

2.open C:\ProgramData\ssh\sshd_config as an Administrator:
  notepad sshd_config

3.add new port:
  Port 1234
  
4.change the sshd_config file:
  PermitRootLogin no
  PubkeyAuthentication yes
  PasswordAuthentication no
  \#GSSAPIAuthentication no
  \#Match Group administrators
  \#   AuthorizedKeysFile __PROGRAMDATA__/ssh/administrators_authorized_keys

5.Allow the SSH port in Windows Firewall. By default, the server is using port 22. Run this command in an elevated command prompt:
  netsh advfirewall firewall add rule name="SSHD Port" dir=in action=allow protocol=TCP localport=22
  
6.Connect by the SSH client
  ssh -i path\to\id_rsa -p portnumber username@ip
  e.g.: ssh -i .\id_rsa -p 1234 John@123.123.123.123
