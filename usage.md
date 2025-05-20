# Usage guide

This document describes how to run Python scripts in my toolkits on your images, using the **mmcrop.py** script in the **momomagick** toolkit. Please refer to [the installation guide](https://github.com/takushim/momodoc/blob/main/installation.md) to install **momomagick** and other toolkits.


**Note:** If you are an expert, feel free to proceed your own way. You are the "root"!

## Assumptions
* Required software is installed, including Python and Git.
* You have successfully installed the **momomagick** toolkit in the `bin` folder within your home folder.
* You have created a Python virtual environment **momo** in the `venv` folder within your home folder and installed the required Python packages in it.
* The `PATH` and `PATHEXT` environment variables are configured.
* Python scripts (`.py` files) are associated with `Python`.
* You can open the folder storing your images using File Explorer.

## Step-by-step instructions
1. Open a PowerShell window in the folder containing your images.

![Ppen PowerShell](https://github.com/takushim/momodoc/raw/main/images/open_powershell.png)

2. Make sure that you are in your image folder by checking the prompt. When you select a folder before opening a PowerShell window, File Explorer will launch PowerShell for the selected folder.

![PowerShell prompt](https://github.com/takushim/momodoc/raw/main/images/powershell_prompt.png)

3. Activate the virtual environment.
```
. $HOME/venv/momo/Scripts/Activate.ps1
```
4. If you haven't set up the `PATH` and `PATHEXT` environment variables, run the following commands to configure these variables.
```
$env:PATHEXT = "${env:PATHEXT};.PY"
$env:PATH = "${env:PATH};${HOME}/bin/momomagick"
```
5. You can confirm that all settings are correct using:
```
mmcrop.py --help
```
6. Run Python scripts from my toolkits. For example:
```
mmcrop.py -R 0 0 256 256 your_image.tif
```
7. If you have set up the CUDA environment, some scripts run faster using a GPU with the `-g 0` option:
```
mmregister.py -g 0 -e Rigid -t Powell time_lapse_3d.tif
```
