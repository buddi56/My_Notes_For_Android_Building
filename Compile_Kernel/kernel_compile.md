# These commands are only for compiling kernel

    export CROSS_COMPILE=$(pwd)/bin/aarch64-linux-android-

    export ARCH=arm64 && export SUBARCH=arm64

*Use either of the 4 commands to compile. Above 2 commands are used only once. With every error we use either of the 4 commands below.*

    make clean

    make mrproper

    make oppo6771_17061_defconfig

    make -jn

**OR**

    mkdir -p out

    make O=out clean

    make O=out mrproper

    make O=out oppo6771_17061_defconfig

    make O=out -jn
    
    
 **Note:** To get *n* use ```nproc```
