## Super computers
#JOMAA2023

## Spirit 

1. Connect to Spirit:
```
ssh -XY username@spiritx1.ipsl.fr
```

2. Launch a job:

When you first connect to Bridges you connect what is called the "login node" We don't actually want to perform any of our computational work on the login node of Bridges, instead we need to connect to a "compute node." Compute nodes are much more powerful and have far fewer users connected to them than the login node.

Bridges uses a tool called Slurm to run processes, or "jobs," on compute nodes. There are a lot options for running jobs using SLURM on Bridges for instance an interactive job This just connects us to a compute node so we can run commands on the command line. Run the following command to start an interactive session:

```
salloc --time=6:00:00 --mem=9g --x11 bash
```
or you can create a bash file as follows (in .pbs file)

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

here you can write whaterever commands you want

```
Sometimes this process can take a while Bridges is very busy, but it usually shouldn't take more than 10 seconds. 
<br>You should see some output that looks like this:

```consule
salloc: Granted job allocation 204453
salloc: Waiting for resource configuration
salloc: Nodes spiritx64-5 are ready for job
```

## SLURM Commands
slqueue: query the list of pending and running jobs. By default it reports the list of pending jobs sorted by priority and the list of running jobs sorted separately according to the job priority. The most relevant job states are running (R), pending (PD), completing (CG), completed (CD) and cancelled (CA). The TIME field shows the maximum execution time of the job

scancel: cancel a pending or running job.
