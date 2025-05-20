# Installation guide

This document describes how to install the Python toolkits in my repositories, using `momomagick` as an example. Please replace `momomagick` with the toolkit name you want to install, such as `momotrack` or `tanitracer`. All of the Python toolkits in my repositories can be installed and used by following these instructions.

**Note:** You can skim this document if you are an expert. My toolkits have a simple directory (folder) structure that follows standard Python conventions. 

## Install necessary software 

Download and install the following programs:

* [Python 3.11.1 or later](https://www.python.org)
* [Git](https://git-scm.com/)
* [Fiji](https://imagej.net/software/fiji/) -  used to view output images

**Note:** On the first page of the Python installer, check `Add python.exe to PATH` if you are not familiar with the command-line interface (see the image below). You don't need to do this for the Git installer, as it typically configures the PATH environment automatically.

![Add python.ext to PATH](https://github.com/takushim/momodoc/raw/main/images/add_python_to_path.png)

## Clone my repository  
1. Open a PowerShell window. At each step of this guide, make sure that your current folder has changed correctly by checking the folder name shown in the prompt.

![PowerShell prompt](https://github.com/takushim/momodoc/raw/main/images/powershell_prompt.png)

2. Create a folder where you want to install the toolkit. I prefer creating a `bin` folder in the home folder.
```
mkdir $HOME/bin
```
3. Move to the folder.
```
cd $HOME/bin
```
4. Clone my repository in the folder.
```
git clone https://github.com/takushim/momomagick.git
```

## Set up the virtual environment for the toolkit
Here, you will install the required Python packages (libraries) in a virtual environment named **momo** using `pip`. This environment can be shared across all my toolkits.

Although you could install these packages directly to the Python system, it is highly recommended to use [a virtual environment](https://docs.python.org/3/library/venv.html) to install packages.


1. Open PowerShell.
2. Create a folder to store your virtual environment. I prefer creating a `venv` folder in the home folder.
```
mkdir $HOME/venv
```
3. Move to the folder.
```
cd $HOME/venv
```
4. Create a virtual environment named **momo**. If `python` is not in your `PATH`, provide the full path to `python.exe`.
```
python -m venv momo
```
5. Activate the **momo** virtual environment.
```
. $HOME/venv/momo/Scripts/Activate.ps1
```
6. Update pip (optional). Activating the virtual environment makes `pip` available in your `PATH`. The `py` launcher will run `python.exe` in your environment.
```
py -m pip install pip -U
```
7. Install the required packages. Below is an example command for **momomagick**.
```
pip install numpy pandas scipy Pillow tifffile ome-types statsmodels transforms3d progressbar2
```

## Set up the CUDA environment (optional)
Some scripts can run faster using an NVIDIA GPU and CuPy.
1. Set up the CUDA environment using guides for [Windows](https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html) or [Linux](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).
2. Install the `cupy` package using `pip`. For CUDA version 12, for example:
```
pip install cupy-cuda12x
```
3. Use the Python script with the `-g 0` option. The number may vary if your PC has multiple GPU devices.

## Set up the environment variables for the Windows system
This is the most **tricky** part. You need to configure the Windows system to recognize Python scripts as **commands**. Otherwise, Windows will launch a new command line window and close it immediately after running a script.
1. Ensure that Python files (.py) are associated with Python. You can check this by opening the properties of any Python file in one of my toolkits. To locate Python files easily, enable "Show file name extensions" in File Explorer (this is also a good security habit).

![File type association for Python files](https://github.com/takushim/momodoc/raw/main/images/python_opens_with.png)

![Show file name extensions](https://github.com/takushim/momodoc/raw/main/images/file_name_extensions.png)

2. Open the environment variables setting window. This can be found by searching for “Edit environment variables for your account” in Windows Settings. Add `.PY` to the `PATHEXT` variable. This allows PowerShell to treat Python scripts as executable commands.

![Environment variables window](https://github.com/takushim/momodoc/raw/main/images/user_variables.png)

![PATHEXT](https://github.com/takushim/momodoc/raw/main/images/pathext_variable.png)

3. Add the path to **momomagick** to your PATH environment variable. This lets PowerShell find the scripts in this toolkit.

![PATH](https://github.com/takushim/momodoc/raw/main/images/path_variable.png)

4. Alternatively, you can temporarily set the environment variables in your current PowerShell session:
```
$env:PATHEXT = "${env:PATHEXT};.PY"
$env:PATH = "${env:PATH};${HOME}/bin/momomagick"
```
5. Now, you are ready to follow the [usage guide](https://github.com/takushim/momodoc/blob/main/usage.md)
