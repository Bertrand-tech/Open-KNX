# Introduction

To build an OpenKNX project locally on you PC you need first follow the steps in

Local build get usually an other Application Number and Application Version for the ETS-Application (knxprod-file). This prevents any corruption of released OpenKNX ETS-Applications in ETS. You should not import an change ETS-Application (knxprod-file) with the same version in ETS until you exactly know what you do.

If you just want to update/bugfix existint firmware for an existing (released) ETS-Application, see section [For experienced users](#for-experienced-users)

## Preparation (just once)

The OpenKNX project comes with preconfigured Build and Deployment tasks. It is convenient to add these tasks to keyboard shortcuts. 

* **Tasks: Run Build Task** allows the execution of a build. This is assigned to the keyboard shortcut <Ctrl>+<Shift>+B. If not, do the assignment.
* **Tasks: Run Test Task** allows the execution of supporting tasks. We suggest to assign it to keyboard shortcut <Ctrl>+<Shift>+T.
* **File: Reveal in File Explorer** shows the selected file or directory in Windows file explorer. We suggest to assign it to keyboard shortcut <Ctrl>+<Shift>+R

In the rest of the document keyboard shortcuts are mentioned. If you decide not to assign them, you have always to use F1 + Task name (in bold) from the list above.

## Create knxprod-file

From Visual Studio, you can create the necassary knxprod-file directly. Just press <Ctrl>+<Shift>+T and select the according OpenKNXproducer task, i.E.

**OpenKNXproducer** OAM-LogicModule

The knxprod file is created and available in the src directory of the project. You should run knxprod genaration at least once before you build the project to get correct defines for the build.

## Build

From Visual Studio, you can just build or build and upload your files to the device. If you press <Ctrl>+<Shift>+B, a dropdown appears with all possible build environments. The names are project dependant and chosen by the responsible developer, but common names are

* **Build RP2040** OAM-LogicModule
* **Upload USB RP2040** OAM-LogicModule
* **Build SAMD** OAM-LogicModule
* **Upload USB SAMD** OAM-LogicModule

If you choose one of them, the according project (or subproject) is build and uploaded (if requested).

## For experienced users

If you want to change/fix any firmware errors in a released version of an OpenKNX module, you can do this by building the release first and **afterwards** changing the sources and building locally with the build described above. If you press <Ctrl>+<Shift>+T, a dropdown appears with all possible Release versions. In most cases it is just

**Build-Release** OAM-LogicModule

But there might be also other releases (for VPM there is als an **Build-Big** OAM-PresenceModule). Just select the according release and the build starts. Building a release might take longer, because all hardware platfomrs are build here.

>Important: Do not distribute a modified release. If you want to distribute any modified version of OpenKNX products, rebuild everything with new ApplicationNumber and ApplicationVersion for ETS.

