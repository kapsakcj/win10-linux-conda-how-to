# win10-linux-conda-how-to
A tutorial on how to set up a Linux environment on a computer running Windows 10. Followed by how to install and use (bio)conda.

[I started this tutorial on a Twitter thread](https://twitter.com/CurtisKapsak/status/974737312155422721) but after a suggestion, decided to create a repository to document everything. This way people can comment, suggest changes, make recommendations, etc. to improve the tutorial!

I've created this tutorial to help out anyone interested in doing bioinformatics analyses but they:
  * Do not have a Mac or a computer running Linux (running natively)
  * Do not have access to a high performance computing cluster/server/whatever you want to call it
  * Hate VirtualBox or other similar virtual computing applications (robs your computer's resources!)
  * Have a computer running Windows 10, 64-bit (with a 64-bit CPU!)
  * Want access to a Linux command line
 
 ## Outline/Table of Contents
   1. [Install Linux Subsystem on your computer running Windows 10](#step-1-install-linux-subsystem-on-your-computer-running-windows-10)
   2. [Install your Linux Distribution of Choice](#step-2-install-your-linux-distribution-of-choice)
   3. [Install conda into your new Linux environment using Miniconda](#step-3-install-conda-into-your-new-linux-environment-using-miniconda)
   4. [Set up Bioconda channels in conda](#step-4-set-up-bioconda-channels-in-conda)
   5. [Use conda to install any of the 3000+ bioinformatics tools available in the Bioconda repository](#step-5-use-conda-to-install-any-of-the-3000-bioinformatics-tools-available-in-the-bioconda-repository)

 
#### Why should I use (bio)conda? 
Check out the pre-print on bioconda here:
[Bioconda: A sustainable and comprehensive software distribution for the life sciences | bioRxiv](https://www.biorxiv.org/content/early/2017/10/27/207092)

  * reproducability
  * ease of software installation

I use it mainly because it is a solution for the mess that is installing dependencies (dependency = software needed to run other software) for bioinformatics software. This program will save you a big headache when trying to run your favorite software - quality control tools, genome assemblers, data visualization, basecallers, etc. There are lots of software out there and each will require installing a specific combination of required dependencies. Bioconda will take that headache away by essentially building a pseudo-environment for you to work in, as if every dependency were already installed (and installed correctly!!). 

Need to change from Python v.2.7 to 3.6? No problem. No need to un-install the old version of python that you installed previously, you can install the newer version right on top, and remove it (and revert to the old version) simply with one command when you're ready to. The other beautiful thing is that Bioconda works on most, if not all operating systems.
 
  
### PC Requirements
  * x64 based processor, AKA 64-bit processor (check by going to **Settings** -> **System** -> **About** -> **Device Specifications** -> **System type**)
  * Windows 10 build version 16215 or later. [How to check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number)
    * [It is possible to use an earlier build of Win10, but I've not tried this before.](https://docs.microsoft.com/en-us/windows/wsl/install-win10#for-anniversary-update-and-creators-update-install-using-lxrun)
  * Storage space - A good bit of storage space needs to be available on your computer's storage drive, at least 2 GB for basic installation, + however much space you need for your data and additional programs
    * For Miniconda—400 MB disk space is required
  * CPU/RAM - you'd likely be OK with a 2 core CPU and maybe 4GB RAM, but the more core's and RAM, the better. My computer has 4-core CPU (i5 Intel) and 8GB of RAM, and it runs just fine. The nice thing about this setup is that the Linux subsystem runs natively and has access to all of your computers resources (unlike Virtualbox, which robs your system's resources just to run)
  
### General Resources
  * [Microsoft's documentation on the Windows 10 Linux subsystem](https://docs.microsoft.com/en-us/windows/wsl/about)
  * [FAQ's about the Windows 10 Linux subsystem](https://docs.microsoft.com/en-us/windows/wsl/faq)
  * [What's the difference between conda, anaconda, and miniconda?](https://bioconda.github.io/faqs.html#conda-anaconda-minconda)
  * [Bioconda: A sustainable and comprehensive software distribution for the life sciences | bioRxiv](https://www.biorxiv.org/content/early/2017/10/27/207092)
  * [Using Bioconda -- Bioconda documentation](https://bioconda.github.io/)
  * [Managing conda environments](https://conda.io/docs/user-guide/tasks/manage-environments.html)
  * [WARNING from Microsoft: Do not change Linux files using Windows apps and tools](https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/)
  

 
 
## Step 1. Install Linux Subsystem on your computer running Windows 10
The first step is to install the Linux Subsystem into your Windows 10 OS. I've copied and modified the bulk of these instructions (and a few images) from Microsoft's documentation found here: https://docs.microsoft.com/en-us/windows/wsl/install-win10 . Thanks to the folks at Microsoft for putting together this documentation and making it publicly available on github!

Enable the "Windows Subsystem for Linux" optional feature and reboot.

1. Open PowerShell as Administrator and run:
    ``` PowerShell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    ```

2. Restart your computer when prompted.

## Step 2. Install your Linux Distribution of Choice
### Fall Creators Update (Win10 build 16215) and later: Install from the Microsoft Store

> This section is for Windows build 16215 or later.  Follow these steps to [check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number).  For earlier versions of Windows 10, follow [these instructions using lxrun](https://docs.microsoft.com/en-us/windows/wsl/install-win10#for-anniversary-update-and-creators-update-install-using-lxrun).

1. Open the Microsoft Store and choose your favorite Linux distribution. I use **Ubuntu**, because it comes pre-loaded with everything needed to install conda (for example python 3.5), but most distributions should be OK.

If you use a distribution other than Ubuntu, ensure that it has the following programs installed:
  * Python 2.7, 3.4, 3.5 or 3.6
  * pycosat
  * PyYaml
  * Requests

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

#### !!Warning about editing linux files using Windows apps and tools!!
I highly reccommend that you scan through this before proceeding. Basically don't mess with any of the linux files using Windows apps or tools. https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/

You can access your computer's storage drives in the directory `/mnt/[name of your drive]` usually`/mnt/c` or `/mnt/d` for saving files there and if you would like to access them from your Linux command line.

## Step 3. Install conda into your new Linux environment using Miniconda
The bulk of these directions were copied and modified from here: https://conda.io/docs/user-guide/install/linux.html 

### Linux Environment Requirements
  * Python 2.7, 3.4, 3.5 or 3.6
  * pycosat
  * PyYaml
  * Requests 
    * The Ubuntu distribution available through Microsoft store is 16.04 LTS, comes pre-loaded with these (python 3.5.1). If your distribution doesn't have these, running `sudo apt upgrade` or `sudo apt-get upgrade` may install them.

You'll need to download the correct version of Miniconda (miniconda = conda installer) dependent upon which version of python is installed into your linux environment. Check by running `which python`, `python --version`, or `python3 --version`. Here's the list of all Miniconda installers. https://conda.io/miniconda.html 

You'll want the "Linux 64-bit" installer, for the correct version of python that is installed into your Linux environment.

1. Open your newly created Linux environment and download the miniconda installer bash script by entering the following in the terminal (this command is for the Linux 64-bit python 3.5/3.6 script):
```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
2. Run the bash script:
```
bash Miniconda3-latest-Linux-x86_64.sh
```
3. Follow the commands as prompted by the conda installer. You can accept the defaults, and change them later if you want.
4. To make the changes take effect, close and then re-open the terminal window
5. Test your installation by running:
```
conda list
```
For a successful installation, a list of installed packages appears.

## Step 4. Set up Bioconda channels in conda
The bulk of these instructions were copied and modified from here: https://bioconda.github.io/#using-bioconda

1.  Run the following three commands from the terminal (IN THIS ORDER!!!)
```
conda config --add channels defaults
conda config --add channels conda-forge
conda config --add channels bioconda
```
You should see a warning message after running the first command, but that is OK, simply proceed with the three commands. You will not see any message or output after entering the third command. That is OK, it just means that there is no output to the terminal.

## Step 5. Use conda to install any of the 3000+ bioinformatics tools available in the Bioconda repository
Some examples of tools available on Bioconda's Repository. Just try searching for you favorite tools here: https://bioconda.github.io/recipes.html:
  * fastqc - A quality control tool for high throughput sequence data
  * SPAdes - An assembly toolkit containing various assembly pipelines
  * bwa - The BWA read mapper
  * samtools - Tools for dealing with SAM, BAM and CRAM files
  * bamtools - C++ API and command-line toolkit for working with BAM data
  * bedtools - a swiss army knife for genome arithmetic
  * albacore - basecaller for Nanopore sequence data
  * poretools - toolkit for extracting fastq data and producing run QC figures and statistics
  * unicycler - de novo assembler used for hybrid short and long read assemblies
  * abricate - mass screening of contigs for antibiotic resistance genes
  * bamtools - C++ API and command-line toolkit for working with BAM data
  * bedtools - a swiss army knife for genome arithmetic
  * and many, many more

I'm going to demonstrate this using the bacterial de novo genome assembly tool, Unicycler, as an example but feel free to try it out with any of the tools listed in the bioconda repository: https://bioconda.github.io/recipes.html

1. Create an environment for Unicycler, by running the following at the terminal:
```
conda create --name unicyclerEnvironment
```
Now there is a new "environment" created for running unicycler. It currently is empty and has almost nothing installed in the environment, but that will come in a second. I'll use this to specify the versions of all the dependencies I need installed.

2. Now activate the environment with:
```
source activate unicyclerEnvironment
```

You will now see `(unicyclerEnvironment)` in parenthesis show up prior to the normal ``user@host~:`` tag that is shown at the terminal before you type anything. This means that you are currently working in the environment that you created, running the versions of software that were installed with your program of interest.

3. Install Unicycler and all of its dependencies :) into the current environment using:
```
(unicyclerEnvironment) user@host~:$ conda install unicycler
```

4. Check the list of programs installed by using:
```
(unicyclerEnvironment) user@host~:$ conda list
```
You can also run this same command from your root environment, but with different syntax:		
```
conda list -n unicyclerEnvironment
```
You should see a list of all dependencies that are installed into the specific environment that you are working in. There are many ways to change and manipulate this list. See the one liners below.

5. Most programs have a short command used to check the installation, either by running `programName --version` or `programname --help` or sometimes even simply `program name`. In the case of Unicycler, Run the following:
```
(unicyclerEnvironment) user@host~:$ unicycler --help
```
6. When you would like to leave the unicyclerEnvironment and return to the root environment, use the following command:
```
(unicyclerEnvironment) user@host~:$ source deactivate 
```
You can combine many of the above steps with simple one-liner! This is actually the **preferred route**, because you can install multiple tools at once, and ensure that conda installs compatible dependencies.
```
conda create -n spadesEnv spades=3.11.1 bwa samtools fastqc
```


### Useful conda one-liners (with `mynewenvironment` as an example). I pulled most of these from here: https://conda.io/docs/user-guide/tasks/manage-environments.html
- Create new conda environment
```
conda create -n mynewenvironment
```
- Activate environment (start working within the environment)
```
source activate mynewenvironment
```
- Deactivate environment (leave environment)
```
(mynewenvironment} user@host~:$ source deactivate
```
- Add a package to an existing environment, for example scipy
```
conda install -n mynewenvironment scipy
```
- Add a package to an existing environment with a specific version, like scipy 0.15.0
```
conda install -n mynewenvironment scipy=0.15.0
```
- List all environments that have been created by the user
```
conda info --envs
```
- List all packages currently installed into the environment
```
(mynewenvironment) user@host~:$ conda list
```
- Remove a conda environment and all of its installed packages
```
conda remove --name mynewenvironment --all
```

## Bonus Goodies
  * [How to change the font and window colors so that your eyes don't bleed from Microsoft's awful choice of default colors](https://medium.com/@jgarijogarde/make-bash-on-ubuntu-on-windows-10-look-like-the-ubuntu-terminal-f7566008c5c2)
  * 
