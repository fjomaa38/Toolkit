## How to connect to servesrs without typing the password each time?
#JOMAA_2023

1. create an ssh key using: 
```bash 
ssh-keygen -t rsa
```
2. in file .ssh/config (vi .ssh/config) write:

```bash 
Host server_abbreviation # you choose it   
ProxyCommand ssh -qX username@server_name nc IP portnb 
User user_name
GatewayPorts yes
```
Now you can connet to the server using the "server_abbreviation" you have choosed 

 Path to SSH folder in the local machine:  /Users/username/.ssh/
