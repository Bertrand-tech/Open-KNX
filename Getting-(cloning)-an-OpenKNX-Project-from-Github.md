# Introduction

OpenKNX reuses already implemented functionality, especially according ETS-Applications. We call them modules. 
A module is published as a github project, which means, that we have dependencies between different github project.
To allow an easy cloning of OpenKNX projects, we have a restore infrastructure, which automatically clones all dependent projects
and configures them to the "last released" version or to developer state.

In case you haven't setup your development environment, first follow the steps in [Installation of OpenKNX development environment](https://github.com/OpenKNX/OpenKNX/wiki/Installation-of-OpenKNX-development-environment-for-PlatformIO-(PIO))
 
## Cloning

Open powershell

> **IMPORTANT:** If you are not using developer mode, it has to be a powershell with administrator privileges.

Go to your favorite development directory. For PIO the default is `~/Documents/PlatformIO/Projects`
In case it is not there (because you never created a PlatformIO project before), you can create ist with

    mkdir ~/Documents/PlatformIO/Projects

Nevertheless, you can work in any directory you like.

Create a directory OpenKNX and go to this directory

    mkdir OpenKNX
    cd OpenKNX

Clone your target OpenKNX PIO project, in this example it is our LogicModule:

    git clone https://github.com/OpenKNX/OAM-LogicModule.git

Go to the restore directory of cloned Project and execute `Restore-Project.ps1` 

    cd OAM-LogicModule/restore
    ./Restore-Project.ps1

> Important: If there is no restore directory, you are done, no further steps necessary! In this case the project is self contained and handles all dependencies as a git-subtree. Not all projects can be created this way, that's why both variants exist.

> Important: You have to start this script inside this directory. A command like `./OAM-LogicModule/restore/Restore-Project.ps1` will not work.

Alternatively you can execute this script from File-Explorer by right-clicking on the file and selecting "Execute with Powershell" (only in Developer Mode).

Now the script clones all dependent objects. This may take some time. 

Afterwards the project is just on your PC, probably not in a state you can build it. You should go to one of the states described in the following chapters.

## Go to "hash state" or "detached state"

Run the script `Restore-Checkout-Hash.ps1` from an powershell command line or from file explorer.

    ./Restore-Checkout-Hash.ps1 

Now all dependent projects are checked out to the state of last successful release build. This means, with this state the project was successfully build last time. This does not guarantee a successfull build, because the root project itself might got new commits after last successful build. 
To ensure a successful build, you have to checkout your root project to any Release-Tag (see git history) and run `Restore-Checkout-Hash.ps1` afterwards.

The intention of this script: We have a historical state of our root project (i.e. one with a release tag) and we want bring all dependent projects to exact the state in which this project was build.

## Go to "branch state" or "developer state"

Run the script `Restore-Checkout-Branch.ps1` from an powershell command line or from file explorer.

    ./Restore-Checkout-Branch.ps1 

In this state you have the newest version of all branches of all subprojects the project was build with. This does not mean, that the project will sucessfully build now, because any of these branches might got new commits after the root project was committed.

The intention of this script: As a developer I want to have the most current state of the root and all dependent subprojects. Because the current project might depend on differnt branches of subprojects, these branches are checked out for me.


