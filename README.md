# U6143_ssd1306 Driver for Ubuntu ARM64 (Raspberry Pi) & Install Script
_forked from `UCTRONICS/U6143_ssd1306`_

SSD1306 Modified Driver and Installer Script for UCTRONICS U6143 Raspberry Pi Rackmount Case.
Modified source project to display temps in Celsius and dynamically configure system hostname in header file using installer script.
Installer script also configures systemd rc-local functionality and enables OLED screen using the modified parameters at boot.
## Installing
Download installer script, set executable, and run with Bash:
For now - run as root!
```
sudo -i
wget https://raw.githubusercontent.com/brad07x/U6143_ssd1306_ubuntu/master/install.sh
chmod +x install.sh
./install.sh
```
# Original Project Readme
***
# U6143_ssd1306
## Preparation
```bash
sudo raspi-config
```
Choose Interface Options 
Enable i2c

##  Clone U6143_ssd1306 library 
```bash
git clone https://github.com/UCTRONICS/U6143_ssd1306.git
```
## Compile 
```bash
cd U6143_ssd1306/C
```
```bash
sudo make clean && sudo make 
```
## Run 
```
sudo ./display
```

## Add automatic start script
- Open the rc.local file 
```bash
sudo nano /etc/rc.local
```
- Add command to the rc.local file
```bash
cd /home/pi/U6143_ssd1306/C
sudo make clean 
sudo make 
sudo ./display &
```
- reboot your system

## For older 0.91 inch lcd without mcu 
- For the older version lcd without mcu controller, you can use python demo
- Install the dependent library files
```bash
sudo pip3 install adafruit-circuitpython-ssd1306
sudo apt-get install python3-pip
sudo apt-get install python3-pil
```
- Test demo 
```bash 
cd /home/pi/U6143_ssd1306/python 
sudo python3 ssd1306_stats.py
```

## Custom display temperature type 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the TEMPERATURE_TYPE variable to change the type of temperature displayed. (The default is Fahrenheit)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/select_temperature.jpg)


## Custom display IPADDRESS_TYPE type 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the IPADDRESS_TYPE variable to change the type of IP displayed. (The default is ETH0)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/select_ip.jpg)

## Custom display information 
- Open the U6143_ssd1306/C/ssd1306_i2c.h file. You can modify the value of the IP_SWITCH variable to determine whether to display the IP address or custom information. (The custom IP address is displayed by default)
![EasyBehavior](https://github.com/UCTRONICS/pic/blob/master/OLED/custom_display.jpg)





