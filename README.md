# win10-linux-conda-how-to
A tutorial on how to set up a Linux environment on a computer running Windows 10. Followed by how to install (bio)conda.

[I started this tutorial on Twitter](https://twitter.com/CurtisKapsak/status/974737312155422721) but after a suggestion, decided to create a repository to document everything. This way people can comment, suggest changes, make recommendations, etc. to improve the tutorial!

I've created this tutorial to help out anyone interested in doing bioinformatics analyses but they:
  * Do not have a Mac or a computer running Linux (running natively)
  * Do not have access to a high performance computing cluster/server/whatever you want to call it
  * Hate VirtualBox or other similar virtual computing applications (robs your computer's resources!)
  * Have a computer running Windows 10
  
Requirements
------
  * x64 based processor, AKA 64-bit processor (check by going to **Settings** -> **System** -> **About** -> **Device Specifications** -> **System type**)
  * Windows 10 build version 16215 or later. [How to check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number)
    * [It is possible to use an earlier build of Win10, but I've not tried this before.](https://docs.microsoft.com/en-us/windows/wsl/install-win10#for-anniversary-update-and-creators-update-install-using-lxrun)
  
General Resources
-------
  * [Microsoft's documentation on the Windows 10 Linux subsystem](https://docs.microsoft.com/en-us/windows/wsl/about)
  * [FAQ's about the Windows 10 Linux subsystem](https://docs.microsoft.com/en-us/windows/wsl/faq)
  
  
## Step 1. Install Linux Subsystem on your computer running Windows 10
The first step is to install the Linux Subsystem into your Windows 10 OS. I've copied these instructions from Microsoft's documentation found here: https://docs.microsoft.com/en-us/windows/wsl/install-win10 Thanks to the folks at Microsoft for putting together this documentation and making it available on github!

Enable the "Windows Subsystem for Linux" optional feature and reboot.

1. Open PowerShell as Administrator and run:
    ``` PowerShell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    ```

2. Restart your computer when prompted.

## Step 2. Install your Linux Distribution of Choice
### Fall Creators Update and later: Install from the Microsoft Store

> This section is for Windows build 16215 or later.  Follow these steps to [check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number).  For earlier versions of Windows 10, follow [these instructions using lxrun](https://docs.microsoft.com/en-us/windows/wsl/install-win10#for-anniversary-update-and-creators-update-install-using-lxrun).

1. Open the Microsoft Store and choose your favorite Linux distribution.      
    Here are links directly to the store installers:
    * [Ubuntu](https://www.microsoft.com/store/p/ubuntu/9nblggh4msv6)
    * [OpenSUSE](https://www.microsoft.com/store/apps/9njvjts82tjx)
    * [SLES](https://www.microsoft.com/store/apps/9p32mwbh6cns)
    * [Kali Linux](https://www.microsoft.com/store/apps/9PKR34TNCV07)
    * [Debian GNU/Linux](https://www.microsoft.com/store/apps/9MSVKQC78PK6)

    ![](UbuntuStore.png)

2. Select "Get"

    > **Troubleshooting: Installation failed with error 0x80070003**  
    > The Windows Subsystem for Linux only runs on your system drive (usually this is your C: drive).  Make sure that new apps are stored on your system drive.  
    > Open **Settings** -> **Storage** -> **More Storage Settings: Change where new content is saved**
    > ![](AppStorage.png)
    
3. Once the download has completed, select "Launch".  
    This will open a console window.  Wait for installation to complete then you will be prompted to create your LINUX user account.
    ![](UbuntuInstall.png)
    
    > **Troubleshooting: Installation failed with error 0x8007007e**  
    > This error occurs when your system doesn't support Linux from the store.  Make sure that:
    > * You're running Windows build 16215 or later. [Check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number).
    > * The Windows Subsystem for Linux optional component is enabled and the computer has restarted.  [Make sure WSL is enabled](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#confirm-wsl-is-enabled).


    
5. Create your LINUX username and password.  This user account has no relationship to your Windows username and password and hence can be different. [Read more](https://docs.microsoft.com/en-us/windows/wsl/user-support).

You're done!  Now you can use your Linux environment.
