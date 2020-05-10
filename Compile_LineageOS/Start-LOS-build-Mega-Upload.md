# Compile Lineage OS

**Initial phase: install git and repo tools**

0. Check for updates, always.

        sudo apt-get update && sudo apt-get upgrade

1. Install required packages.

        sudo apt-get install android-tools-adb android-tools-fastboot git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip python

2. Make a directory to place repo tool.

        mkdir ~/bin

3. Set path to use repo tool anywhere (i.e., repo can be used universally)

        PATH=~/bin:$PATH

4. Downoad the repo tool.

        curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

5. Make the tool executable.

        chmod a+x ~/bin/repo

**Second phase: Set Environment**

6. Install required packages for Android/Lineage development.

        sudo apt-get install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline6-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev

7. Make a working directory aka, you will store Android source code here and compiling takes place in this dir. You can give any name for the dir. Using ROM name with its version is easy and convinent.

        mkdir working_directory

8. cd into the working directory.

        cd working_directory

9. Input Git username or simply enter random value

        git config --global user.name "Your Git UserName here"

10. Input Git Mail or simply enter random one

        git config --global user.email "Your Git Mail address"

11. Initialise repo.

        repo init -u git://github.com/LineageOS/android.git -b lineage-16.0

12. Get nproc value

        nproc (get "n" from here)

13. Use the above ```nproc``` vaue to sync source code using multiple threads. This takes lot of time, depends on the nproc value and Internet Speed.

        repo sync -j(nproc) --force-sync

**Third phase: Setting ccache and Jack**

__a. ccache in Android 9 and below__

14. Use CCACHE. If you want to use Ccache then execute below 3 commands. CCache is used to quicken build speed.

        export USE_CCACHE=1

15. Input the storage yu want to use for ccache. Here I used 50G (means 50 GB). If you build for multile devices then this is enough, but for 1 device you can use 25GB and this storage is permanent.

        prebuilts/misc/linux-x86/ccache/ccache -M 50G
        
        export CCACHE_COMPRESS=1
        
__b. ccache in Android 10__

        export USE_CCACHE=1; export USE_CCACHE_EXEC=$(command -v ccache); ccache -M 50G;
        
 where 50G is the space allocated to cache.
        
16. Setup Jack, use below command

        export ANDROID_JACK_VM_ARGS="-Xmx16g -Dfile.encoding=UTF-8 -XX:+TieredCompilation"
        
Remember to replace 16 in -Xmx16g with half the value of your RAM. Eg: If I have 16GB RAM then it is -Xmx8g.

**Fourth phase: Start compiling**

17. Start build

        . build/envsetup.sh

18. Compile. Example *brunch lineage_CPH1859-eng*

        brunch ROMName_DeviceName_BuildVariant  -j(nproc)
        
Example:

        brunch lineage_CPH1859-userdebug -j8

or

        make bacon -j(nproc)

**Fifth phase: Uploading to Mega (through terminal)**

19. Install following package:
        
        sudo apt-get install megatools
  
20. Now use below command to upload file.
        
        megaput <file> -u <username> -p <password>

**Note:** *Mega is not allowing new users (accounts made after 11/06/2018) to upload files. The memory you use for ccache is permanent (You cannot use that storage for storing files).*
