# sen2cor installation

Version 2.0.6 is available on the anaconda cloud (https://anaconda.org/terradue/sen2cor).

I install 2.2.1 manually into a new conda environment.

My home directory:
```bash
HOMEDIR="/gpfs/data1/huanggp/bdv"
```

## Create conda environment

```bash
conda create -n s2a_221 python=2.7.11
```

## Download sen2cor

```bash
cd $HOMEDIR/.conda/envs/s2a_221
wget http://step.esa.int/thirdparties/sen2cor/2.2.1/sen2cor-2.2.1.tar.gz
tar -xvzf sen2cor-2.2.1.tar.gz
cd sen2cor-2.2.1
python setup.py install
```

There will be several prompts during this installation. One will ask you to confirm the SEN2COR_HOME directory, so you will need to decide whether to accept the default or not. If not, enter 'n', and the next prompt will ask you to enter the SEN2COR_HOME directory of your choice.

## Configure

Environment variables specific to a conda env can be saved in the ```etc``` directory (see http://conda.pydata.org/docs/using/envs.html for more information on this). In the installation above, the etc/conda/activate.d directory was already created, so we just need to create the required env_vars.sh script in that directory. In this script, we will insert a command to activate the L2A_Bashrc script, so that this happens every time we activate our s2a_221 conda environment.

```bash
cd $HOMEDIR/.conda/envs/s2a_221
cd etc/conda
touch activate.d/env_vars.sh
```

Open this file in a text editor and enter the following:

```bash
#!/bin/bash
....



At this point, activating our environment (```source activate s2a_221```) and running ```L2A_Process --help``` should work. But it seems I am still missing some python modules (which I thought should have been installed with sen2cor...).

```
conda install pytables psutil scipy scikit-learn hdf5
```

