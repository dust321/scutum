[![Join the chat at https://gitter.im/K4YT3X-DEV/SCUTUM](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/K4YT3X-DEV/SCUTUM?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![status](https://travis-ci.org/K4YT3X/SCUTUM.svg)](https://travis-ci.org/K4YT3X/SCUTUM)

# SCUTUM Firewall

#### Current Version: 2.5.1

</br>

#### Current Version Change log:
1. Interfaces are now controlled by a new interface controller class
2. SCUTUM GUI is now avaliable for testing

![scutum_gui](https://user-images.githubusercontent.com/21986859/29802954-bb3475f2-8c46-11e7-8c21-efae476ac5a6.png)

#### TODO:
1. Finish up developing a stable version for SCUTUM GUI


#### Recent Changes:
1. Added option to choose whether to delete the installer file after installation
2. Fixed arptables detection errors on some Linux distributions
3. Fixed some bugs that is unnoticeable :D
4. Added installation wizard for avalon framework when not installed. supports 3 methods of automatic installation
5. Added arptables detection and installation wizard
6. Added enable / disable / start option

<br>
<p align="center"> 
<img src="https://user-images.githubusercontent.com/21986859/27760965-d228eda6-5e29-11e7-9ba6-3d9cc0408fd8.png">
</p>

## What is SCUTUM?
<b>Long story short, ARP firewall. It automatically adds gateways to the whitelist on connect and blocks everthing else to avoid potential threat.</b>

SCUTUM is an ARP firewall that **prevents your computer from being ARP-spoofed** by other computers on LAN. SCUTUM controls "arptables" in your computer so it accepts ARP packets only from the gateway. This way, when people with malicious intentions cannot spoof your arp table. SCUTUM also prevents other people from detecting your device on LAN if SCUTUM is used with properly configured TCP/UDP firewall.

SCUTUM is also capable of handling tcp/udp/icmp traffic with iptables. You can choose to enable this feature during installation. However, a more professional firewall controller like UFW is recommended. They can handle traffic with more precision.

<br>

## Usage & Installation
You should run a installation before running it for the first time for setting up configuration files. 
<b>I am not sure if portable version is necessary. If you think this should be changed, raise an issue and I will change it.</b>
#### Installation
~~~~
git clone https://github.com/K4YT3X/SCUTUM.git
cd SCUTUM/
sudo python3 scutum.py --install  # scutum.py deletes itself after installation
cd ../
rm -rf SCUTUM/
~~~~

#### GUI Usage
~~~~
ENABLE: Enable SCUTUM (Start spontaneously)
DISABLE: Disable SCUTUM (Never start spontaneously)
DISABLE (Temporarily): Disable SCUTUM until the next time connected to a network
~~~~


#### Usage
This should be easy
SCUTUM starts <b>automatically</b> by itself after installation
~~~~
$ sudo scutum              # Start SCUTUM Normally
$ sudo scutum --start      # Start SCUTUM Manually for once even it it's disabled
$ sudo scutum --enable     # Enable SCUTUM (Start automatically on connect)
$ sudo scutum --disable    # Disable SCUTUM (Don't start automatically on connect)
$ sudo scutum --reset      # Reset SCUTUM (Allow ALL ARP packages temporarily)
$ sudo scutum --purgelog   # Purge SCUTUM logs
$ sudo scutum --install    # Run scutum installation wizard and install SCUTUM into system
$ sudo scutum --uninstall  # Remove SCUTUM from system completely 
~~~~

<br>

## SCUTUM Workflow:
#### postconnect
1. Connect to Wi-Fi
2. Accept all ARP packets
3. Cache gateway MAC address by establishing a socket connection with a timeout of 0
4. Add Gateway MAC to exception
5. DROP all ARP packets

[Finished]


#### postdisconnect
1. Accept all ARP packets

[Finished]
