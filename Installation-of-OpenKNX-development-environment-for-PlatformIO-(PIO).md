Tested on Windows 10, Windows 11 should work, too!

# Installation steps

Set your Windows to "Developer Mode" [as described here](https://consumer.huawei.com/en/support/content/en-us15594140/)

<kbd>![Developer mode](https://user-images.githubusercontent.com/14316138/224475367-bf24628f-eca6-48a6-9e12-7cd1860a9ae1.png)</kbd>

> **Information:** Developer Mode allows you to work with symbolic links in Windows without administrator privileges. OpenKNX PIO projects use symbolic links and developer mode makes it easy to work with. If you don't want or are not allowed to use developer mode, you can still compile OpenKNX PIO projects, but then you have to ensure, that all github clone operations are executed from a Windows Command Prompt (cmd) with administrator privileges. Other shells (like git bash) will not work with symlinks without developer mode.

Enable also the execution of PowerShell-Scripts (the last entry on the same settings page as developer mode). This enables all scripts you need for a successfull setup.
 
<kbd>![PowerShell](https://user-images.githubusercontent.com/14316138/224475331-ef281a62-44fe-42a3-9d44-cbce93e19d2a.png)</kbd>


Download and install git from [https://git-scm.com/downloads](https://git-scm.com/downloads) with symbolic link support. This is one of the last advanced settings in the whole sequence of settings and the only one that has to be changed from the default:

<kbd>![Git-Settings](https://user-images.githubusercontent.com/14316138/192711629-a89ecbe9-4158-441d-81b8-ef08c4b24b85.png)</kbd>
 
> **IMPORTANT:** Be sure, that you check the option "Enable symbolic links". If you already installed git without this option, reinstall it.

Go to a console window (i.e. Command Prompt/Eingabeaufforderung, Win+R cmd) and setup git to use symbolic links:

    git config --global core.symlinks true

> **IMPORTANT:** The above command has no effect, if git was not installed with "Enable symbolic links" option.

The actual status can be verified using the following command:

    git config --global core.symlinks

Download and install the newest release of OpenKNX-Tools from [https://github.com/OpenKNX/OpenKNXproducer/releases](https://github.com/OpenKNX/OpenKNXproducer/releases) according to installation instructions described in OpenKNX-Wiki [https://github.com/OpenKNX/OpenKNX/wiki/Installation-of-OpenKNX-tools](https://github.com/OpenKNX/OpenKNX/wiki/Installation-of-OpenKNX-tools)

Download and install visual studio code from [https://code.visualstudio.com/download](https://code.visualstudio.com/download) (User installer, 64 bit)

Start visual studio code

Go to extensions (Ctrl-Shift-X)

Enter "platformio" in search field

Install "PlatformIO IDE" extension

Wait until installation is finished, do the necessary reload window afterwards (may take some time)

Now you have all parts installed to checkout and build an OpenKNX PIO project.

# Verify installation

You can do this with any OpenKNX module followint the instructions in [Getting-(cloning)-an-OpenKNX-Project-from-Github](/OpenKNX/OpenKNX/wiki/Getting-(cloning)-an-OpenKNX-Project-from-Github). We suggest to take [OAM-LogicModule](/OpenKNX/OAM-LogicModule).

If you executed all cloning instructions and the build was successfull, everything is fine and you are done.

If not, you can do the following checks:

Go to the lib directory of cloned LogicModule-project and look at its content

    cd OAM-LogicModule/lib
    dir

You should see some files indicating, that they are links to other directories. The presentation depends on your favorite shell, in Command Prompt it is:

    22.09.2022  15:18    <SYMLINKD>     knx [..\..\knx]
    22.09.2022  15:18    <SYMLINKD>     OGM-Common [..\..\OGM-Common]

If these are normal files (without the information in square brackets) or the filetype is not \<SYMLINKD\>, something went wrong.
You shoud run again the script `Restore-Project.ps1` in `restore` directory, which should repair this situation.

> **IMPORTANT** Be careful, the filetype might be \<SYMLINK\> missing the "D", this is wrong but can be easily overlooked.

The known cases for a missing \<SYMLINKD\>:

* git was installed/reinstalled without the symbolic link support
* Developer Mode is off
* one (or more) of the above **git clone** commands failed
* the setting **git config --global core.symlinks true** did not work
* the setting **git config --global core.symlinks true** worked, but is overridden by a user setting **git config --user core.symlinks false** or a workspace setting **git config core.symlinks false** 
