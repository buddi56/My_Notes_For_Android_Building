# Compile Lineage OS

**Initial phase: install git and repo tools**

1. First step is to install required packages for Git.

        sudo apt-get install android-tools-adb android-tools-fastboot git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip python

2. Make a directory to place repo tool.

        mkdir ~/bin

3. Set path to use repo tool anywhere (i.e., repo can be used universally)

        PATH=~/bin:$PATH

4.Downoad the repo tool.

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

        git config --global user.name "Your Git User Name here"

10. Input Git Mail or simply enter random one

        git config --global user.email "Your Git Mail address"

11. Initialise repo.

        repo init -u git://github.com/LineageOS/android.git -b lineage-16.0

12. Get npro value

        nproc (get "n" from here)

13. Use the above ```nproc``` vaue to sync source code using multiple threads. This takes lot of time, depends on the nproc value and Internet Speed.

        repo sync -jn --force-sync

**Third phase: Start Compiling**

14. Use CCACHE. If you want to use Ccache then execute below 3 commands. CCache is used to quicken build speed.

        export USE_CCACHE=1

15. Input the storage yu want to use for ccache. Here I used 50G (means 50 GB). If you build for multile devices then this is enough, but for 1 device you can use 25GB and this storage is permanently used.

        prebuilts/misc/linux-x86/ccache/ccache -M 50G
        
        export CCACHE_COMPRESS=1

16. Start build

        . build/envsetup.sh

17. Compile. Example *brunch lineage_CPH1859-eng*

        brunch ROMName_DeviceName_BuildVariant  -j(nproc)

or

        make bacon -j(nproc)

**Fourth phase: Uploading to Google Drive (Only for people using Google Console aka, GCD)**

18. The below step is for Developers who use Google Console for building ROMs. After building, you can upload your ROM to Google Drive, it is fast and convinent.

19. Go to root directory

        cd ~

20. Download GDrive app

        wget https://docs.google.com/uc?id=0B3X9G...xport=download

21. Change name of the file

        mv uc\?id\=0B3X9GlR6EmbnWksyTEtCM0VfaFE gdrive

22. Make the file executable

        chmod +x gdrive

23. Install the file

        sudo install gdrive /usr/local/bin/gdrive

24. chacking whether gdrive installed or not.

         gdrive list

25. Upload file to gdrive.

          gdrive upload /home/MachineName/working_directory/out/target/product/DeviceName/ROM.zip

Example: ```gdrive upload /home/ynaveenk_0513/lineageos_16/out/target/product/CPH1859/lineage_CPH1859-ota-eng.ynaveenk_0513.zip```

Uploading to Gdrive is very quick, it takes less than 5 secons. 

**Note:** *To use gdrive you have to provide Google Drive access. Also the memory you use for ccache is permanent (You cannot use that storage for storing files).*

