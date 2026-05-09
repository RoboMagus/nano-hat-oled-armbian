# NanoHAT OLED for Armbian - Python3 RC
NanoHAT OLED and GPIO Button Control for Armbian. This documentation contains installation and upgrade instructions.

## Disclaimer

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

## Getting Started

### Prerequisites

Enable i2c0:

Add `i2c0` to the line `overlays=` in `/boot/armbianEnv.txt`. Reboot the system for the changes to take effect.

### Dependencies
Install the dependences from APT:
```
sudo apt -y install \
  libjpeg-dev \
  libfreetype6-dev \
  python3 \
  python3-dev \
  python3-libgpiod \
  python3-pillow \
  python3-pip \
  python3-setuptools \
  python3-smbus \
  python3-wheel \
  fonts-dejavu \
  zlib1g-dev
```
And install `image` and `pillow` from PIP:
```
sudo pip3 install \
  image \
  pillow
```

### Get the Code
Clone from GitHub:
```
cd /tmp
git clone https://github.com/RoboMagus/nano-hat-oled-armbian
```

### Install
Make the program directory:
```
sudo mkdir -p /usr/share/nanohatoled
```

Copy the program files:
```
sudo mv /tmp/nano-hat-oled-armbian/oled-start3.py /usr/share/nanohatoled/
sudo mv /tmp/nano-hat-oled-armbian/splash.png /usr/share/nanohatoled/
```

Copy service file:
```
sudo mv nanohatoled.service /etc/systemd/system
sudo systemctl daemon-reload
sudo systemctl enable nanohatoled.service
```

Reboot the system for the changes to take effect.

## Troubleshooting

### Compatibility with BakeBit and NanoHatOLED
This does not require the FriendlyARM BakeBit or NanoHatOLED software to be installed. If this has already been installed you will need disable it.
```
sudo nano /etc/rc.local
```
Then find the lines:
```
/usr/local/bin/oled-start
exit 0
```
And comment out the `oled-start` line by adding `#` at the start of the line, so the lines look like this:
```
# /usr/local/bin/oled-start
exit 0
```
Save these changes by pressing `ctrl+x`, `ctrl+y` and `enter` as prompted at the bottom of the screen.   
   
Reboot the system for the changes to take effect.
```
sudo reboot now
```
