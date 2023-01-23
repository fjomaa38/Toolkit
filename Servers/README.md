## How to connect to servesrs without typing the password each time?
#JOMAA_2023

1. create an ssh key using: 
```bash 
ssh-keygen -t rsa
```
Path to SSH folder in the local machine: /Users/username/.ssh/

2. in file .ssh/config (vi .ssh/config) write:

```bash 
Host server_abbreviation # you can choose any name   
ProxyCommand ssh -qX username@domain nc IP portnb 
User user_name
GatewayPorts yes
```
Now you can connet to the server using the "server_name"
(type "server_name" and hit enter)

Good job :)

