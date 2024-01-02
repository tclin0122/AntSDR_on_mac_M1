# AntSDR_on_mac_M1

## Intro
Set up the environment to operate AntSDR(PlutoSDR)

## Tool sets [1]
1. Libiio
2. libad9361-iio
3. pyadi-iio
4. HoRNDIS

### Install Libiio
Install from scratch
```
brew install libserialport
cd ~
git clone --branch v0.23 https://github.com/analogdevicesinc/libiio.git
cd libiio
mkdir build && cd build
cmake -DPYTHON_BINDINGS=ON ..
make -j$(nproc)
sudo make install
```
change source file
```
vim ~/.zshrc
```
add path
```
export PATH="/Library/Frameworks/iio.framework/Tools:$PATH"
```
source the file
'''
source ~/.zshrc
'''

### Install LibAD9361-iio
```
cd ~
git clone https://github.com/analogdevicesinc/libad9361-iio.git
cd libad9361-iio
mkdir build && cd build
cmake ..
make -j$(nproc)
sudo make install
```
### Install pyadi-iio
```
cd ~
git clone --branch v0.0.14 https://github.com/analogdevicesinc/pyadi-iio.git
cd pyadi-iio
pip3 install --upgrade pip
pip3 install -r requirements.txt
sudo python3 setup.py install
```
### Install HoRNDIS [2]
1. Switching to "Reduced Security" mode
 - Shut down your Apple Silicon Mac.
 - Press and hold down the power button until the text under the Apple logo says "Loading startup options…", then let go.
 - Select "Options".
 - You are now in recoveryOS — enter your password if it asks.
 - Go to Utilities → Startup Security Utility.
 - Select "Reduced Security" and enable Allow user management of kernel extensions from identified developers".
 - Shut down your Apple Silicon Mac.
2. Disabling SIP (System Integrity Protection)
 - Follow steps 2〜4 from above.
 - Go to Utilities → Terminal.
 - Type in the following to fully disable SIP: csrutil disable
 - Reboot your Apple Silicon Mac.
3. Download and install [Xcode](https://developer.apple.com/xcode/resources/)
4. Run the following in a Terminal session
```
git clone --recursive https://github.com/jwise/HoRNDIS.git
cd Development/HoRNDIS/
xcodebuild -sdk macosx -configuration Release
sudo cp -rv build/Release/HoRNDIS.kext /Library/Extensions/
```
5. Go to System Preferences → Security & Privacy and approve the HoRNDIS kernel extension.
6. Reboot, connect the USB of the AntSDR


## Reference
[1]https://pysdr.org/content/pluto.html 

[2]https://github.com/jwise/HoRNDIS/issues/146

