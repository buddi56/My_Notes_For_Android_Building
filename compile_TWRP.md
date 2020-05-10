# Compiling TWRP (aka Team Win Recovery Project)

**Phase 1: Install repo and set path in one go**

Installing repo and setting path is similar to the one shared in compiling ROM. So downloading repos tools, setting path can be done in one go.

      sudo apt-get update; sudo apt-get install android-tools-adb android-tools-fastboot git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc unzip python bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev; mkdir ~/bin; PATH=~/bin:$PATH; curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo; chmod a+x ~/bin/repo

**Phase 2: Compiling**

      mkdir working_dir;

b. Change to that dir to start proceedings.

      cd working_dir;

c. Setup git values.

      git config --global user.name "Your Git UserName here"; 

      git config --global user.email "Your GitMail";

 d. Initialize the repo.

      repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b branchName
 
 Eg:

      repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0

 Start syncing sources.

      repo sync -j$(nproc)

 You can use --force-sync if it is required.

 e. Compile using below command in one go.

      export ALLOW_MISSING_DEPENDENCIES=true; . build/envsetup.sh; lunch omni_CodeName-buildvariant; mka recoveryimage -j$(nproc)

Eg:

      export ALLOW_MISSING_DEPENDENCIES=true; . build/envsetup.sh; lunch omni_CPH1861-eng; mka recoveryimage -j8 | tee build.log


 Note: That the pipe with tee is used to capture build log. For more info you can use this [link](https://raw.githubusercontent.com/buddi56/android_device_oppo_CPH1859/CPH1859_Android_9/Imp_for_first_time_builders.txt) for TWRP compilation.
