# sen2cor installation

Version 2.0.6 is available on the anaconda cloud (https://anaconda.org/terradue/sen2cor). I started by creating a conda environment which I call "s2c\_206", just installing gdal to start (other dependencies will come with sen2cor). When that is done, activate the environment using ```source activate s2c\_206``` and install sen2cor from the terradue repo.

```bash
conda create -n s2c_206 gdal
source activate s2c_206
conda install -c terradue sen2cor=2.0.6
```
After installing many dependencies, this failed for me near the end of the installation (something to do with needing root access to Spacewalk repo's on our Red Hat distribution). By this time the environment had been created with the dependencies, so I got around this issue by migrating to the environment directory and downloading and installing sen2cor=2.0.6 directly inside this directory.

```bash
cd /my_home_dir/.conda/envs/s2c_206
wget http://s2tbx.telespazio-vega.de/sen2cor/sen2cor-2.0.6.tar.gz
cd sen2cor-2.0.6
python setup.py install
```

As you can see in the messages from the installation process, you need to migrate to your sen2cor home directory (set in the prompt) and ```source L2A_Bashrc```. This script sets 3 environment variables that are needed to run the sen2cor pre-processing utilities. You can insert that command in your .bashrc file so that it runs everytime you log in.

If all went well, you should be able to run the ```L2A_Process``` script by now. Run it with the ```--help``` flag, and if there are no errors, you (probably) have a working installation!

Alas, I still didn't -- I got a warning message saying my HDF5 headers did not match my install version. I haven't been able to figure this one out quite yet, but there is an environment variable - ```HDF5_DISABLE_VERSION_CHECK``` that can be set to ```1``` to ignore this prompt. This can actually be set specifically for the current conda environment by creating an ```env_vars.sh``` script. 

```bash
cd /my_home_dir/.conda/envs/s2c_206/etc/conda/activate.d
touch env_vars.sh
gedit env_vars.sh
```

`env_vars.sh` should look like this:

```bash
#!/bin/bash
export HDF5_DISABLE_VERSION_CHECK=1
```

There is an analogous deactivate script for when you deactivate this environment:

```bash
cd /my_home_dir/.conda/envs/s2c_206/etc/conda/deactivate.d
touch env_vars.sh
gedit env_vars.sh
```

...which should look like this:

```bash
#!/bin/bash
unset HDF5_DISABLE_VERSION_CHECK
```


## References



##################################################

I install 2.2.1 manually into a new conda environment.

My home directory:
```bash
HOMEDIR="/gpfs/data1/huanggp/bdv"
```

## Create conda environment

```bash
conda create -n s2a_221 gdal pytables psutil PIL scipy scikit-learn matplotlib hdf5
```

Including gdal in the list because of ```libcom_err.so.3``` errors.

Need to fix hdf5 version warning. Set LD\_LIBRARY\_PATH instead of disabling warnings?? "Headers are 1.8.16, library is 1.8.17"


## Download sen2cor

```bash
cd $HOMEDIR/.conda/envs/s2a_221
wget http://step.esa.int/thirdparties/sen2cor/2.2.1/sen2cor-2.2.1.tar.gz
tar -xvzf sen2cor-2.2.1.tar.gz
cd sen2cor-2.2.1
python setup.py install
```

sen2cor 2.0.6 is available at http://s2tbx.telespazio-vega.de/sen2cor/sen2cor-2.0.6.tar.gz

There will be several prompts during this installation. One will ask you to confirm the SEN2COR\_HOME directory, so you will need to decide whether to accept the default or not. If not, enter 'n', and the next prompt will ask you to enter the SEN2COR\_HOME directory of your choice.

Install version 2.0.6 downgraded several packages in my conda environment, including gdal, which caused issues with a missing libcom\_err library. Reinstall gdal with ```conda install gdal``` fixed this (but could also contribute to the HDF5 version warnings I got later...?)

## Configure

Environment variables specific to a conda env can be saved in the ```etc``` directory (see http://conda.pydata.org/docs/using/envs.html for more information on this). In the installation above, the etc/conda/activate.d directory was already created, so we just need to create the required env_vars.sh script in that directory. In this script, we will insert a command to activate the L2A_Bashrc script, so that this happens every time we activate our s2a\_221 conda environment.

```bash
cd $HOMEDIR/.conda/envs/s2a_221
cd etc/conda
touch activate.d/env_vars.sh
```

Open this file in a text editor and enter the following:

```bash
#!/bin/bash
export HDF5_DISABLE_VERSION_CHECK=1
```


At this point, activating our environment (```source activate s2a_221```) and running ```L2A_Process --help``` should work. But it seems I am still missing some python modules (which I thought should have been installed with sen2cor...).

```
conda install pytables psutil scipy scikit-learn hdf5
```

