The crspy package uses an old version of Numpy only compatible with Python version 3.19, so before installing it you will have to create a new environment with the mentioned Python version.

Follow the steps below to prepare the working environment.

## Install another version of Python

Safer than downgrading or upgrading is installing other versions of Python on the same system.

To install Python 3.9:

```
# Add the deadsnakes repository
me@mydevice:~$ sudo add-apt-repository ppa:deadsnakes/ppa
```

```
# Update package lists
me@mydevice:~$ sudo apt update
```

```
# Install Python 3.9
me@mydevice:~$ sudo apt install python3.9
```

## Install the venv package and create a venv virtual environment

```
# Install the venv package for Python 3.9
me@mydevice:~$ sudo apt install python3.9-venv
```

```
# Make a folder for venv virtual environments
me@mydevice:~$ mkdir ~/.venvs
```
```
# Create a new venv virtual environment with Python 3.9 in it
me@mydevice:~$ python3.9 -m venv ~/.venvs/my-venv-name
```

```
# Activate the new venv
me@mydevice:~$ source ~/.venvs/my-venv-name/bin/activate
(my-venv-name) me@mydevice:~$
```

## Check versions within the venv virtual environment

```
# Check the Python version inside the venv:
(my-venv-name) me@mydevice:~$ python -V
Python 3.9.18
```

```
# Check the Pip version inside the venv:
(my-venv-name) me@mydevice:~$ pip3 --version
pip 21.2.4 from /home/me/.venvs/my-venv-name/lib/python3.9/site-packages/pip (python 3.9)
```

## Deactivate the venv virtual environment

```
(my-venv-name) me@mydevice:~$ deactivate
me@mydevice:~$
```

## Install the crspy package to your venv virtual environment

There are some PC requirements that may be required first, namely hdgf5 headers and netcdf4 system files. If errors occur during install, install these first.

In my experience, I have not had these errors. But, if there are errors, run the following commands.

```
# Install HDF5 header files
(my-venv-name) me@mydevice:~$ sudo apt-get install libhdf5-dev
```

```
# Install NetCDF4 library
(my-venv-name) me@mydevice:~$ sudo apt-get install libnetcdf-dev
```

```
# Run the command
(my-venv-name) me@mydevice:~$ pip install crspy
```

```
# Upgrade your pip version
(my-venv-name) me@mydevice:~$ pip install --upgrade pip
``` 

## Create a new directory in your local machine

There is an example on the author's GitHub account, so before performing the example create a new directory on your local machine.

```
# Create a new directory:
(my-venv-name) me@mydevice:/mnt/c/Users/user-name/Desktop$ mkdir main_folder
```

```
# Change the current working directory to the new directory
(my-venv-name) me@mydevice:/mnt/c/Users/user-name/Desktop$ cd main_folder
(my-venv-name) me@mydevice:/mnt/c/Users/user-name/Desktop/main_folder$
```

## Install Jupyter notebook

Before running the example, you must install jupyter notebook by executing the following code.

```
# Install the classic Jupyter Notebook
(my-venv-name) me@mydevice:/mnt/c/Users/user-name/Desktop/main_folder$ pip install notebook
```

```
# To run the notebook:
(my-venv-name) me@mydevice:/mnt/c/Users/user-name/Desktop/main_folder$ jupyter notebook
```

> To access the server, open the URL shown in your browser, create a new Notebook and select the kernel.

Now, follow the same steps written in the author's Notebook called run_crspy_workthrough located in the author's GitHub repository in the crspy_example folder.


## Adding data

In this step you must create an account in CDS climate copernicus to download the dataset. After creating your account you will know your UID and API key, this information must be included in a file called .cdsapirc stored in `(my-name-venv) me@mydevice:/home/me$`


The .cdsapirc file contains the following information:

```
	url: https://cds.climate.copernicus.eu/api/v2
	key: <UID>:<API>
	verify: 0
```

change <UID> and <API> to your respective credentials in your account. And accept the terms and conditions of the CDS website.

The next change to make is to add a command line to the python script called additional_metadata.py. This file is located in `(my-venv-name) me@mydevice:~/.venvs/my-venv-name/lib/python3.9/site-packages/crspy$`

In the file scroll down to the AGB data section, line 300 or so, before print("Downloading...") you must add the following command line:

```
nld=nld['config']
```

because the variable nld was not declared in that function. Then save the change and restart your kernel in Jupyter Notebook.

> NB: These changes are done only once.

Then, follow the steps below from the author of the example.


## References:

https://stackoverflow.com/questions/70422866/how-to-create-a-venv-with-a-different-python-version

https://jupyter.org/install

https://cds.climate.copernicus.eu/

https://github.com/ecmwf/cdsapi

https://github.com/danpower101/crspy

https://github.com/danpower101/crspy_example
