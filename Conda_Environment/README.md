## How to download miniconda on your machine and setup your environment?
#JOMAA_2021 

Don't hestitate to check out the official sites of 
* [Anaconda](https://www.anaconda.com/products/individual) 
* [Minconda](https://docs.conda.io/en/latest/miniconda.html) 
* [Environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

### 1. Installing conda:

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
                                               

### 2. Creating a new environment:
```bash
conda create --name env_name  python=3.8 
# Don't forget to replace env_name by your environment name :p
```
> To activate environment: 
> </br> `conda activate env_name`
> </br> ##Note: to automatically activate the environment add to **.bashrc:** `conda activate env_name`
> </br> </br>To deactivate environment: `conda deactivateenv_name` 
> </br> </br>Check environment: `python -m pip freeze`
> </br> </br>Check available environment: `conda info --envs`
> </br></br>To remove other environments: `conda env remove --n env_name`
> </br></br> *Extra set up* 
> </br>#If you'd prefer that conda's base environment not be activated on startup:
> </br>`conda config --set auto_activate_base false`
   >>check with:
   >> </br>`conda config --show | grep auto`

## 3. Creating an environment from an environment.yml file
1. Create tan environment from an existing environment.yml file:
`conda env create -f environment.yml` 
> The first line of the `yml` file sets the new environment's name. For details
2. Activate the new environment: `conda activate myenv`
3. Verify that the new environment was installed correctly: `conda env list`

## 4. Saving an environment

* To have the exact version of packages on the machine you are using and their dependencies, which will allow you to have exactly the same environment:

>`conda list --explicit > projet_v0.txt` #txt format
></br>`conda env export > projet_v0.yml` # yml format  

* To save the the names of the installed packages with their version number if specified:

>`conda env export --from-history > projet_v0_fh.yml` # Allows sharing your environment across different platforms/OS
></br></br>--> Notes: 
></br>-Some packages are not always available across all platforms. 
></br>-To isure that all packages continue working in future you should always specify all version numbers as there are often conflicts between some packages (e.g., version 0.6.4 of proplot does not work with version 3.3 of matplotlib, or cartopy does not work with the latest version 3.9 of python...)
></br></br> So using exiting environment may not always work on other platforms. But if you update any package by mistake and you find that the new version is incompatible with other packages you can still restore your environment if you already saved it ^^ 
