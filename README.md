Tesla M Manifest
================

Setting up your build environment for Ubuntu/Mint
=================================================

Prepare your Java environment
-----------------------------
In terminal:
------------
```
sudo apt-get purge openjdk-\* icedtea-\* icedtea6-\*
sudo apt-get update
sudo apt-get install openjdk-7-jdk
```
Check your version: 
```
java -version
```
Should see something similar too:
```
java version "1.7.0_65"
OpenJDK Runtime Environment (IcedTea 2.5.3)
OpenJDK 64-Bit Server VM (build 24.65-b04, mixed mode)
```
Install some required tools:
----------------------------
```
sudo apt-get install git-core gnupg ccache lzop flex bison gperf build-essential zip curl zlib1g-dev zlib1g-dev:i386 libc6-dev lib32ncurses5 lib32z1 lib32bz2-1.0 lib32ncurses5-dev x11proto-core-dev libx11-dev:i386 libreadline6-dev:i386 lib32z-dev libgl1-mesa-glx:i386 libgl1-mesa-dev g++-multilib mingw32 tofrodos python-markdown libxml2-utils xsltproc readline-common libreadline6-dev libreadline6 lib32readline-gplv2-dev libncurses5-dev lib32readline5 lib32readline6 libreadline-dev libreadline6-dev:i386 libreadline6:i386 bzip2 libbz2-dev libbz2-1.0 libghc-bzlib-dev lib32bz2-dev libsdl1.2-dev libesd0-dev squashfs-tools pngcrush schedtool libwxgtk2.8-dev python
```
If you come into any errors:
----------------------------
```
sudo apt-get update && sudo apt-get upgrade
```
Then try again

Download repo tool and set your path
------------------------------------
```
mkdir ~/bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
Include bashrc in repo tool
---------------------------
```
sudo nano ~/.bashrc
```
Once open: To set the right path for your local bin folder, paste the following code to a new line at the very bottom of the bashrc file, and then save the file using Ctrl+X

Add:
```
export PATH=~/bin:$PATH
export USE_CCACHE=1
```
After saving and closing:
```
source ~/.bashrc (Reload bash variables to include the new path)
```
Install lz4 compression tool:
-----------------------------
```
sudo apt-get install liblz4-tool
```
Tesla-M is built with SaberMod, to install required binaries..
---------------------------------------------------------------
Go to http://oceighty.co/sm/ and download the sabermod-prebuilts .deb file
Install it by running 
```
sudo dpkg -i --force-all sabermod-prebuilts_*****-1.deb
```
Initialize Tesla-M build environment:
-------------------------------------

Open Terminal
```
mkdir tesla && cd tesla
repo init -u git://github.com/Tesla-M/platform_manifest.git -b 6.0
repo sync -j4 
```
"-j is the number of jobs you want give to the download/sync, depending on your system, 4 should be fine on slower systems(i use -j16 on i7, 12Gb)"

Setting up global:
------------------
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
(Just replace the credentials with your own)

When that is done & repo is synced, type:
-----------------------------------------
```
Set ccache : prebuilts/misc/linux-x86/ccache/ccache -M 50G
```
```
. build/envsetup.sh
lunch
Choose your device
make tesla -j#
```
Have Fun!!
----------
