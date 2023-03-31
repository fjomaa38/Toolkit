## Jupyter notebook/ lab
#JOMAA_2021
### 1. Installing jupyter:

```bash
conda install jupyter
```
### 2. Installing jupyter lab:
```
conda install -c conda-forge jupyterlab
python -m ipykernel install --user --name myenv --display-name "Python 3.6 (myenv)"
# don't forget to replace myenv and setup the python version
```
### 3. Launching Jupyter

If you are launching Jupyter on a server you need to make an ssh bridge between your machine and the server to open Jupyter directly on your internet browser. So you have to specify to Jupyter not to open a window on the server and to open Jupyter on a specific port (if needed).

There are two ways to do this, either you specify all this in your command when you run Jupyter, or you create a configuration file.

Note the two options specified in this command. The first command, -no-browser, tells Jupyter not to launch a web browser when it launches. We specify this because we are running Jupyter on a remote machine, which means it can't launch a web browser on your local computer. Instead it launches a text based browser in your terminal that isn't very useful. The second command, ip=0.0.0.0, tells Jupyter to serve the notebook on a public IP address. The default behavior is to only serve the notebook locally (for security reasons), but that doesn't work because we are trying to connect to a remote computer:
* **Command line**

>Here is an example of a command line; XXXX would be your port number  
  ```bash
   jupyter lab --port XXXX --ip 0.0.0.0 --no-browser
   ```

* **Configuration file** (recommended in the sense you don't need everytime to type the above command line ;))

>Generate a configuration file and edit it:

```bash
jupyter notebook --generate-config
vi /home/user/.jupyter/jupyter_notebook_config.py
# add these two lines: 
   c.NotebookApp.open_browser = False 
   c.NotebookApp.ip = '0.0.0.0' 
   c.NotebookApp.allow_origin = '*'
```
-----------------------------------------------------------
After configuration you can launch jupyter by typing this command : 

```bash
jupyter notebook
``` 

Now you will get something similar to:
```ruby
    To access the notebook, open this file in a browser:
        file:///home/XXXX/.local/share/jupyter/runtime/nbserver-4130898-open.html
    Or copy and paste one of these URLs:
        http://hostname@server:7356/?token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
     or http://XXXXX:7356/?token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
Copy one of the generated url into your browser to open jupyter and don't forget to change ***tree*** ,in the url, to ***lab*** 

If you are working on a server you should make a tunnel in your own terminal (on your personal machine) to be able to connect to the browser: 
```bash
ssh -fNL XXXX:hostname:XXXX login@server 
ssh -fNL XXXX:hostname:XXXX -p port_nb login@server  # in case you have to connect to specific port 
```
<br><br>/!\ It's important to have one tunnel to the same server. Otherwise the jupyter will break.
<br> To check the the running processes with ssh use : `ps -aef|grep ssh` you will get:
 ```ruby
 usename     434   225  0 21:26 pts/6    00:00:00 ssh -X login@server
 usename     438     1  0 21:27 ?        00:00:00 ssh -fNL XXXX:hostname:XXXX login@server
 usename     440    30  0 21:28 pts/1    00:00:00 grep --color=auto ssh
 ```
 To delete a process: `kill -9 nb_of_process`
 

