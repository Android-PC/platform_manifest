<img style="text-center" src="https://i.imgur.com/hCQ5em4.png">

Android-PC
-----------------------
Download the Android-PC source code, based on [AOSP](https://android.googlesource.com), & [BlissRoms](https://github.com/BlissRoms/platform_manifest)

---------------------------------------------------

Please read the [AOSP building instructions](http://source.android.com/source/index.html) before proceeding.

-----------------------
What you need to build [Android-PC](https://github.com/Android-PC/platform_manifest)
-----------------------

    Latest Ubuntu LTS Releases https://www.ubuntu.com/download/server
    Decent CPU (Dual Core or better for a faster performance)
    8GB RAM (16GB for Virtual Machine)
    250GB Hard Drive (about 170GB for the Repo and then building space needed)
  
-----------------------

Installing Java 8

    sudo add-apt-repository ppa:openjdk/ppa
    sudo apt-get update && upgrade
    sudo apt-get install openjdk-8-jdk
    update-alternatives --config java  (make sure Java 8 is selected)
    update-alternatives --config javac (make sure Java 8 is selected)
    reboot
    
-----------------------

Grabbing Dependencies
-----------------------

    $ sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip squashfs-tools python-mako libssl-dev ninja-build lunzip syslinux syslinux-utils gettext genisoimage gettext bc xorriso

Initializing Repository
-----------------------

Repo initialization :
    
    ## Releases Repo ##
    $ repo init -u https://github.com/Android-PC/platform_manifest.git -b p9.0

sync repo :

    $ repo sync --no-tags --no-clone-bundle
    
problems syncing? :

    $ repo sync --no-tags --no-clone-bundle --force-sync

Building
--------
PC builds (x86) explained:

    This will build an x86 based .ISO for PCs

    Usage: $ bash build-x86.sh options buildVariants branch/extras
    Options: 
            -c | --clean : Does make clean && make clobber and resets the efi device tree
            -s | --sync: Repo syncs the rom (clears out patches), then reapplies patches to needed repos
            -p | --patch: Just applies patches to needed repos

    BuildVariants: 
            android_x86-user : Make user build
            android_x86-userdebug |: Make userdebug build
            android_x86-eng : Make eng build
            android_x86_64-user : Make user build
            android_x86_64-userdebug |: Make userdebug build
            android_x86_64-eng : Make eng build

    branch: select which bliss branch to sync, default is p9.0
    extras: 
            foss : Build with FDroid & microG
            gapps : Build with OpenGapps (currently disabled)
            none ; Build it naked

    To start, you must first use the -s (--sync) flag, then on following builds, it is not needed.

    $ bash build-x86.sh -s android_x86_64-userdebug (to build the userdebug version)

