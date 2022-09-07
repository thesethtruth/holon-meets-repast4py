# Holon meets Repast4Py
## Set up

### Follow the official docs 
WSL installation guide at [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/wsl/install).

In short; install WSL through the PowerShell:
```powershell
wsl --install
```
> This will install the default distro (Ubuntu). If you which to change the distro use: `wsl --install -d <DistroName>`. If you want to browse the available distros use: `wsl --list --online`.

### Follow the best practice guide
WSL best practice guide at [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/wsl/setup/environment).


### Install the VScode remote development extension 
Remote dev extenstion pack from the [VScode markteplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack).


### Open a project folder in WSL
Hit `CTRL+SHIFT+P` and type `folder WSL` and hit enter to select `Remote-WSL: Open folder in WSL...`.

Create a new folder in your user folder (`/home/$USR/`) called `dev` (for all development projects).

```bash
cd ~        # to home dir
mkdir dev   # create dev folder
cd dev
git pull <<THIS PROJECT>>
```

### Install MiniConda
Installs the Miniconda on your WSL such that we can manage `envs`

```bash
wget https://repo.anaconda.com/miniconda/[VERSION].sh   # get the latest version of miniconda 
bash Miniconda3-[VERSION].sh                            # install miniconda
# proceed to install, type yes to accecpt the conda init option
rm Miniconda3-[VERSION].sh                              # remove the file after installation
```

At time of writing `py39_4.9.2-Linux-x86_64` is the latest version, please check the [Miniconda repo](https://repo.anaconda.com/miniconda) to see if this is still the case. If so, use the following:
```bash
wget https://repo.anaconda.com/miniconda/py39_4.9.2-Linux-x86_64.sh   
bash Miniconda3-py39_4.9.2-Linux-x86_64.sh                            
rm Miniconda3-py39_4.9.2-Linux-x86_64.sh                              
```

Restart your terminal and you should see `(base)` prepended to your terminal line. Check the installation by running `which python`. This should now point to your miniconda installation (`/home/$USR/miniconda3/bin/python`). Now run `conda update -n base -c defaults conda` to update `conda`. 

### Create and activate new conda env

```bash
conda create -n repast
conda activate repast
```

### Install repast4py

```bash
sudo apt-get install mpich          # requirement for compiling the Cython
conda activate repast
env CC=mpicxx pip install repast4py
```

### Run one of the examples

``` bash
cd demomodels/rndwalk
mpirun -n 4 python rndwalk.py random_walk.yaml
```

You can inspect the results in the `./outputs` folder.
