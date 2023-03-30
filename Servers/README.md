## How to connect to servesrs without typing the password each time?
#JOMAA_2023
### 1. Check if there is an existing ssh key
```
ls -al ~/.ssh
```
If the folder contains something like that:
```ruby
-rw-r--r-- 1 XXXXXX XXXXXX   583 Jun 14  2022 config
-rw------- 1 XXXXXX XXXXXX  2602 Dec 14  2021 id_rsa
-rw-r--r-- 1 XXXXXX XXXXXX   571 Dec 14  2021 id_rsa.pub
-rw-r--r-- 1 XXXXXX XXXXXX  9755 Oct 26 14:26 known_hosts
```
then you already have a ssh key, you can move to the next step. Otherwise **create a ssh key using:** 
```bash 
ssh-keygen -t rsa
```
Path to SSH folder in the local machine: /Users/username/.ssh/

### 2. in file .ssh/config (vi .ssh/config) write:

```ruby
Host server_abbreviation # you can choose any name   
ProxyCommand ssh -qX username@domain nc IP portnb  # to get the ip use ifconfig
User username
GatewayPorts yes
```
That's it ;)

Now you can connet to the server without typing your password using:

-the "server_abreviation" that you choosed above
<br>-or ssh -qX username@domain nc IP portnb

Good job :)

