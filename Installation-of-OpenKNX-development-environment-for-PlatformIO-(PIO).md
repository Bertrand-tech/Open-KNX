Tested on Windows 10, Windows 11 should work, too!

# Installation steps

Set your Windows to "Developer Mode" [as described here](https://consumer.huawei.com/en/support/content/en-us15594140/)

> **Information:** Developer Mode allows you to work with symbolic links in Windows without administrator privileges. OpenKNX PIO projects use symbolic links and developer mode makes it easy to work with. If you don't want or are not allowed to use developer mode, you can still compile OpenKNX PIO projects, but then you have to ensure, that all github clone operations are executed from a Windows Command Prompt (cmd) with administrator privileges. Other shells (like git bash) will not work with symlinks without developer mode.

Download and install git from [https://git-scm.com/downloads](https://git-scm.com/downloads) with symbolic link support. This is one of the last advanced settings in the whole sequence of settings:

![Git-Settings](https://user-images.githubusercontent.com/14316138/192711629-a89ecbe9-4158-441d-81b8-ef08c4b24b85.png)
 
> **IMPORTANT:** Be sure, that you check the option "Enable symbolic links". If you already installed git without this option, reinstall it.

Go to a console window (i.e. Command Prompt/Eingabeaufforderung, Win+R cmd) and setup git to use symbolic links:

    git config --global core.symlinks true

> **IMPORTANT:** The above command has no effect, if git was not installed with "Enable symbolic links" option.

Download and install the newest release of OpenKNX-Tools from [https://github.com/OpenKNX/OpenKNXproducer/releases](https://github.com/OpenKNX/OpenKNXproducer/releases) according to installation instructions described in OpenKNX-Wiki [https://github.com/OpenKNX/OpenKNX/wiki/Installation-of-OpenKNX-tools](https://github.com/OpenKNX/OpenKNX/wiki/Installation-of-OpenKNX-tools)

Download and install visual studio code from [https://code.visualstudio.com/download](https://code.visualstudio.com/download) (User installer, 64 bit)

Start visual studio code

Go to extensions (Ctrl-Shift-X)

Enter "platformio" in search field

Install "PlatformIO IDE" extension

Wait until installation is finished, do the necessary reload window afterwards (may take some time)

Now you have all parts installed to checkout and build an OpenKNX PIO project.

# Verify installation

Open your favorite shell

> **IMPORTANT:** If you are not useing developer mode, it has to be Windows Command Prompt (cmd) with administrator privileges.

Go to your favorite development directory. For PIO the default is ~/Documents/PlatformIO/Projects

Create a directory OpenKNX and go to this directory

    mkdir OpenKNX
    cd OpenKNX

Clone an OpenKNX PIO project (in this case it is the OpenKNX LogicModule):

    git clone https://github.com/OpenKNX/OAM-LogicModule.git

Go to the lib directory of cloned project and look at its content

    cd OAM-LogicModule/lib
    dir

You should see some files indicating, that they are links to other directories. The presentation depends on your favorite shell, in Command Prompt it is:

    22.09.2022  15:18    <SYMLINKD>     knx [..\..\knx]
    22.09.2022  15:18    <SYMLINKD>     OGM-Common [..\..\OGM-Common]
    22.09.2022  15:18    <SYMLINKD>     OGM-SensorDevices [..\..\OGM-SensorDevices]

If these are normal files (without the information in square brackets) or the filetype is not \<SYMLINKD\>, something went wrong and you should start over.

> **IMPORTANT** Be careful, the filetype might be \<SYMLINK\> missing the "D", this is wrong but can be easily overlooked.