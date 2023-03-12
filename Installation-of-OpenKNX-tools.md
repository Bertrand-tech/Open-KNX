## Background

OpenKNX will deliver firmware packages, which can be build and uploaded via simple scripts. These scripts will be supported by OpenKNX tools, which have to be installed once. Sometime an Update might be necessary. This Page describes the installation and update procedure.

## Preconditions

OpenKNX uses PowerShell-Scripts for installation of tools, creation of knxprod files and uploading firmware packages to your hardware. Therefore execution of PowerShell-Scripts should be enabled on your system. The easiest way is to do it from Start menu -> Settings -> Update & Security -> for Developers (there its the last entry on the page):

![PowerShell](https://user-images.githubusercontent.com/14316138/224476082-d14187fd-a33b-41d4-82ce-b70789facac8.png)

## Download package

Download the newest OpenKNX tools package from [https://github.com/OpenKNX/OpenKNXproducer/releases](https://github.com/OpenKNX/OpenKNXproducer/releases). Because this zip package contains executable files and a PowerShell script, modern Browsers warn the user, that this download might be dangerours. See the "Explanation" section to understand what the package contains and what is installed.

## Unzip contents

Unzip the downloaded file to any directory.

## Installation

Open the directory with all unzipped files. This directory contains a PowerShell script 
`Install-OpenKNX-Tools.ps1` 
Right-Click on this script and execute it with "Execute with PowerShell". The necessary Tools will be installed.

## Update

An Update of OpenKNX tools is exactly the same as the initial install, foolow the above steps.

## Explanation

The PowerShell script copies all executables contained in tools directory to the users bin directory. If no bin exists, it will be created. Finally a success message is presented.

The executables in tools are:
* OpenKNXproducer.exe - a tool to create a knxprod-File, which can be imported in ETS. The source is available [here](https://github.com/OpenKNX/OpenKNXproducer).
* bossac.exe - a tool to upload firmware to an SAMD microcontroller. The source is available [here](https://github.com/shumatech/BOSSA)

## Remarks

OpenKNXproducer.exe needs a working ETS-Installation on the same PC installed at the standard location of ETS. ETS 5.6 is minimum, ETS 5.7.x and ETS 6 are supported. A Demo-License is sufficient. It does not work with a clean install of ETS. At least one (empty) Project must have been created with this installed ETS.
 