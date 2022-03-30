## How to download miniconda on your machine and setup your environment?
#JOMAA_2021 

Don't hestitate to check the official sites of 
[Anaconda](https://www.anaconda.com/products/individual) and
[Minconda](https://docs.conda.io/en/latest/miniconda.html) 

### 1. To install conda type:

```bash 
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
sh Miniconda3-latest-Linux-x86_64.sh . ~/.bashrc
```
> -->Say yes for the licence 
> </br> </br> Miniconda3 will now be installed into this location: /home/jomaaf/miniconda3
> </br>  #Spefify the directory if different from your home, e.g. to a place where you can have some storage
> </br>  Gricad:[/home/jomaaf/miniconda3] >>> /bettik/jomaaf/miniconda3
> </br>  --> Press ENTER to confirm the location 
> </br>  --> Press CTRL-C to abort the installation - Or specify a different location below 
> </br></br> #Say yes for initialize Miniconda3 by running conda init
> </br>  Do you wish the installer to initialize Miniconda3
> </br>  by running conda init? [yes|no]
> </br>  [no] >>> yes
> </br> </br>  /!\ Close the terminal (with ctrl-d) and reopen a new terminal for changes to take effect
> </br>  activate conda using: `conda config --add channels conda-forge`



                                               Congrats you've installed miniconda ^_^

### 2. Now to create an environment:

```bash
# Don't forget to replace env_name by your environment name :p
conda create --name env_name  python=3.8 (Note: just replace env_name)
```
> To activate environment: 
> </br> `conda activate env_name`
> </br> ##Note: to automatically activate the environment add to **.bashrc:** `conda activate env_name`
> </br> </br>To deactivate environment:
> </br>` conda deactivateenv_name` 
> </br> </br>Check environment
> </br> `python -m pip freeze`
> </br> </br>Check available environment:
> </br> `conda info --envs`
> </br></br>To remove other environments
> </br>`conda env remove --n env_name`
> </br></br> *Extra set up* 
> </br>#If you'd prefer that conda's base environment not be activated on startup:
> </br>`conda config --set auto_activate_base false`
   >>check with:
   >> </br>`conda config --show | grep auto`
