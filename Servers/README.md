## Super computers
#JOMAA2023

## Spirit 
You will read in this page about: 
1. Connect to Spirit
2. Launch a job
3. Slurm commands
4. Launch Jupyter

-----

## 1. Connect to Spirit:

Head nodes adresses by cluster :

- IPSL-SU, spirit:
 > spirit1.ipsl.fr 134.157.176.253 (24 cores, 256GB, EPYC 7402P 24-Core Processor 2.8GHz)
   <br>spirit2.ipsl.fr 134.157.176.200 (24 cores, 256GB, EPYC 7402P 24-Core Processor 2.8GHz)
- IPSL-X, spiritx:
 > spiritx1.ipsl.fr 129.104.53.5 (24 cores, 256GB, EPYC 7402P 24-Core Processor 2.8GHz)
   <br> spiritx2.ipsl.fr 129.104.53.11 (24 cores, 256GB, EPYC 7402P 24-Core Processor 2.8GHz)
- IPSL-G, hal: (GPU small cluster)
 > hal0-ng.obs.uvsq.fr 194.254.41.69 (VM, just access and file transfert, no scientific software on)
 
 Your mesocenter login grants your access to all IPSL ESPRI clusters.
 <br>To connect to a specific cluster head node, you simply execute the command:
```bash
# ssh your_mesocenter_login@head_node_name
# for example
ssh -XY username@spiritx1.ipsl.fr
```
If you wish to connect to the server without typing the passward everytime, check[Passwordless connect](Toolkit/Servers/Password)


## 2. Launch a job:

When you first connect to Bridges you connect what is called the "login node". We don't actually want to perform any of our computational work on the login node of Bridges, instead we need to connect to a "compute node." Compute nodes are much more powerful and have far fewer users connected to them than the login node.

Bridges uses a tool called Slurm (haha yes slurm :\ ) to run processes, or "jobs," on compute nodes. There are a lot of options for running jobs using SLURM on Bridges for instance an interactive job. This just connects us to a compute node so we can run commands on the command line. Run the following command to start an interactive session:

```
salloc --time=6:00:00 --mem=9g --x11 bash
```
or you can create a .pbs file as follows: 
<br>(to run the file type sbatch file.pbs)

```bash 
#!/bin/bash
#
#PBS -N UncompForcing
#
#PBS -j oe
#PBS -l nodes=1:ppn=5     (processor per node)
#PBS -l walltime=5:00:00  (time of the job)
#PBS -l mem=20gb          (requested memory)
#PBS -l vmem=20gb         (virtual memory)

here you can write whatever commands you want
Note: Remove within brackets it is just explanation 

```
Sometimes this process can take a while, when bridge is very busy, but it usually shouldn't take more than 10 seconds. 
<br>You should see some output that looks like this:

```consule
salloc: Granted job allocation 204453
salloc: Waiting for resource configuration
salloc: Nodes spiritx64-5 are ready for job
```
This means that your job number is 204453
<br> and you are connected to spiritx64-5 node

**Note:** Slurm kills the jobs that exceed its maximum execution time.
## 3. SLURM Commands
Here are some SLURM commands that could be useful to go along with your job:

${\color{cyan}slqueue}$ or ${\color{cyan}showq}$: query the list of pending and running jobs. 
<br> By default it reports the list of pending jobs sorted by priority and the list of running jobs sorted separately according to the job priority. The most relevant job states are running (R), pending (PD), completing (CG), completed (CD) and cancelled (CA). The TIME field shows the maximum execution time of the job. The output is something like: 
```ruby
JobId   State   Partition    Username Account Node CPUs Memory Batch    TimeLeft   TimeLimit         Node/Reason
 4253   RUNNING      zen4       xxxx  yyyyy    1    2     6G    0        1:59:55    2:00:00          spirit64-01

```

${\color{cyan}seff}$: check the effeciency of your job.
<br>${\color{cyan}scancel}$: cancel a pending or running job.

```bash
#scancel JobId
scancel 4253 

```
## 4. Launch Jupyter  
To download jupyter on your server checkout [Install Jupyter](/Toolkit/Jupyter/README.md).

Once everything is configured, we can now launch the Jupyter Notebook on the compute node. For more details check out [Install Jupyter](/Toolkit/Jupyter/README.md)
```
jupyter notebook 
```
you will get something like: 

```ruby
    To access the notebook, open this file in a browser:
        file:///home/XXXX/.local/share/jupyter/runtime/nbserver-4130898-open.html
    Or copy and paste one of these URLs:
        http://hostname@server:7356/?token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
     or http://XXXXX:7356/?token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
Copy one of the generated url into your browser to open jupyter and don't forget to change ***tree*** ,in the url, to ***lab*** 

Technically you already have the notebook running but you can't connect to it directly. What we are going to do is open up a new terminal and re-connect to Bridges establishing an SSH Tunnel that allows us to connect your local web browser to the Jupyter Notebook server running deep inside the bowels of Bridges. Note, keep the old terminal open since that is the connection that is running the Jupyter Notebook server, if you close it you will shut down the server.

```bash
ssh -fNL XXXX:hostname:XXXX login@server 
ssh -fNL XXXX:hostname:XXXX -p port_nb login@server  # in case you have to connect to specific port 
```
/!\ It's important to have one tunnel to the same server. Otherwise the jupyter will break.
<br> To check the the running processes with ssh use : `ps -aef|grep ssh` you will get:
 ```ruby
 usename     434   225  0 21:26 pts/6    00:00:00 ssh -X login@server
 usename     438     1  0 21:27 ?        00:00:00 ssh -fNL XXXX:hostname:XXXX login@server
 usename     440    30  0 21:28 pts/1    00:00:00 grep --color=auto ssh
 ```
 To delete a process: `kill -9 nb_of_process`
 
