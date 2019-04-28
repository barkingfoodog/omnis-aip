# omnis-aip
This is a template for building .exe installers for Omnis Studio-based projects on Windows using Caphyon's Advanced Installer.

## Prerequisites
* [Git for Windows](https://git-scm.com/download/win)
* Your [Omnis Studio](http://www.omnis.net)-based application
* [Advanced Installer Professional 15.1 or later](https://www.advancedinstaller.com)
* A [code signing certificate](https://sectigo.com/products/signing-certificates/code-signing)

## Compatibility
This example is built against Omnis Studio 10.0 but should work with any recent version of Omnis Studio.

## Clone the template
Download or clone a copy of this repository. For example, run this command in the *Git Bash* app to clone a copy of the project to a `omnis-aip` folder in `~/Documents`.
```bash
git clone https://github.com/barkingfoodog/omnis-aip.git ~/Documents/omnis-aip
```

## Add files
There are three directories in the `omnis-aip` directory, each with their own README files:
* x64
* x86
* shared

Copy the appropriate files from the Omnis runtime and your own application into these folders. See the individual README files more more details. The installer will install architecture-specific files on 32-bit (x86) and 64-bit (x64) machines, so ensure any files in the `x86` directory has a counterpart in `x64` and vice-versa.

## Customize the installer
Rename the `template.aip` file to match your application. Open this file with Advanced Installer and edit these settings:
 1. **Product Details** -> **Product Details** -> **Name**
 1. **Product Details** -> **Product Details** -> **Version**
 1. **Product Details** -> **Product Details** -> **Publisher**
 1. **Digital Signature** -> **Software Published Certificate** -> **Use from Personal certificate store** -> **Your certificate**
 1. **Install Parameters** -> **Properties** -> **AppDataName** -> Enter the folder under `%PROGRAMFILES%` and `%LOCALAPPDATA%` that will contain your application
 1. **Builds** -> **Output** -> **MSI name** -> A name for the embedded msi
 1. **Builds** -> **Output** -> **EXE** -> A name for the exe installer

### Update the product codes
Under **Product Details** -> **Product IDs** generate a new **Product Code** and **Upgrade Code**. This should be done once for each project.

## Optional customizations
### System Requirements
You can configure the minimum memory, screen resolution, and supported operating systems on which this installer will run:

 1. **Launch Conditions** -> **Supported Operating Systems**
 1. **Launch Conditions** -> **System Requirements** -> **Minimum Physical Memory**
 1. **Launch Conditions** -> **System Requirements** -> **Minimum Screen Resolution**

### License
Edit the `license.rtf` to add your own license agreement that will be displayed during installation.

## Building a package
### GUI
Open your .aip file with Advanced Installer. Click **Home** in the ribbon and click -> **Build**.

### CLI
Adjust the path to Advanced Installer to point to your installed version.
```powershell
"C:\Program Files\Caphyon\Advanced Installer 15.1\bin\x86\AdvancedInstaller.com" /build "[path to your .aip]"
```

## Code signing
Advanced Installer can automatically sign your application and the installer using a puchased code signing certificate. Sectigo sells [code signing certificates](https://sectigo.com/products/signing-certificates/code-signing). Follow their guide to generate and install the certificate on the machine where you will build you installer. Once installed, the certificate will be available under **Digital Signature** -> **Software Published Certificate** -> **Use from Personal certificate store**.

#
# Contributions
Pull requests are most welcome!