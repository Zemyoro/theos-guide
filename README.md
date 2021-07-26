# Theos Guide by Zemyoro
* [Official Guide](https://github.com/theos/theos/wiki/Installation-Linux) (Highly recommended)
* [Ubuntu & WSL Guide](https://github.com/Zemyoro/theos-guide/wiki/Instructions-(For-Ubuntu-based-distros-and-WSL)(Bash-Shell)) (Also below)
* [Wiki](https://github.com/Zemyoro/theos-guide/wiki)

# Instructions (For Ubuntu based distros & WSL) (Bash Shell)
Make sure to run all commands from the code blocks into terminal.


`sudo apt-get install fakeroot git perl clang-6.0 build-essential libtinfo5`

[If you're using WSL and get an error (E.g "E: Unable to locate package clang")](https://github.com/Zemyoro/theos-guide/wiki/WSL-Errors)

**Additionally on WSL:**

`sudo update-alternatives --set fakeroot /usr/bin/fakeroot-tcp`


## Setting up THEOS Environment variable

`echo "export THEOS=~/theos" >> ~/.profile`

`echo "export THEOS=~/theos" >> ~/.bashrc`

`echo "export PATH=$THEOS/bin:$PATH" >> ~/.bashrc`

`echo "alias theos=$THEOS/bin/nic.pl" >> ~/.bashrc`

Optional: `echo "export THEOS_DEVICE_IP=yourdeviceIP" >> ~/.bashrc`

Note: Replace `yourdeviceIP` with your jailbroken device IP.

Restart the terminal before running the commands below

## Clone THEOS

`git clone --recursive https://github.com/theos/theos.git $THEOS`

## Change if using iOS Simulator
`nano $THEOS/vendor/lib/CydiaSubstrate.framework/CydiaSubstrate.tbd` then on line 3, change`iphoneos` to `ios`.

Then, `ctrl + x`, press `y`, then press `enter`

## Get the toolchain
(If you have any issues like "illegal command name" etc... switch terminal to bash)

`curl -LO https://github.com/sbingner/llvm-project/releases/download/v10.0.0-1/linux-ios-arm64e-clang-toolchain.tar.lzma`

`TMP=$(mktemp -d)`

`tar --lzma -xvf linux-ios-arm64e-clang-toolchain.tar.lzma -C $TMP`

`mkdir -p $THEOS/toolchain/linux/iphone`

`mv $TMP/ios-arm64e-clang-toolchain/* $THEOS/toolchain/linux/iphone/`

`rm -r $TMP linux-ios-arm64e-clang-toolchain.tar.lzma`

## Get iOS SDKs

`curl -LO https://github.com/xybp888/iOS-SDKs/archive/master.zip`

`unzip master.zip`

`mv iOS-SDKs-master/*.sdk $THEOS/sdks`

`rm -r master.zip`

`rm -rf iOS-SDKs-master`

## We're Done! Let's run theos

`$THEOS/bin/nic.pl`
or
`theos`
