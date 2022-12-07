# Predator-2022-Wifi
This repo contains a readme which tells you the steps to produce the support for wifi in Linux for Intel killer wifi 6e AX1675x cards

## Steps
- First you have to update your system with internet (use usb tethering from mobile or use ethernet cable)
- Then you have to install intel wifi card backports
`sudo apt install update` and `sudo apt install backport-iwlwifi-dkms` and now reboot your system
- Now you will see wifi adapter will show. But the problem you will be facing is your wifi will only connect 5ghz connections not 2.4 ghz connections
- I found this [link](https://www.linux.org/threads/2-4ghz-wi-fi-network-doesnt-connect-to-ubuntu-20-10.34659/) and see that I have to install and use iwd instead of wpa_supplicant service
- Now install iwd `sudo apt install iwd`
- Then open terminal and write this `
sudo gedit /etc/NetworkManager/conf.d/wifi_backend.conf`. Now paste these into the file 
```
[device]
wifi.backend=iwd
```
- Now stop and disable wpa_supplicant service, open your terminal and Paste these
```
systemctl stop wpa_supplicant.service
systemctl disable wpa_supplicant.service
```
- reboot your system
- Now start and enable iwd service
```
sudo systemctl enable iwd.service
sudo systemctl start iwd.service
```
- reboot your system
- Now restart NetworkManager service by writing this in the terminal
`sudo systemctl restart NetworkManager.service`.

> Now you are done. Now both 2.4ghz and 5ghz wifi connections will work. One issue is it will connect automatically after startup.
