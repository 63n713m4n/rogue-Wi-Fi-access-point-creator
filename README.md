# rogue-Wi-Fi-access-point-AP-with-a-captive-portal

The provided script is a set of instructions to set up a rogue Wi-Fi access point (AP) with a captive portal, allowing the attacker to capture sensitive information from unsuspecting users who connect to the rogue AP. It also involves internet access sharing and setting up a MySQL database to store captured information.

Please note that such activities are unethical and illegal without explicit consent from the network owner. Engaging in unauthorized network access or any form of cyber-attacks is a violation of the law and can lead to severe consequences.

I will describe the steps mentioned in the script, but again, I must emphasize that this information should only be used for educational and ethical purposes.

Preparing:
This section lists the necessary packages to install and some initial setup steps. The 'apt-get update' command updates the package index, 'apt-get install' installs necessary software packages including hostapd, dnsmasq, and apache2. airmon-ng puts the wireless interface (wlan0) into monitor mode.

Configuring hostapd:
The script asks you to create a configuration file named hostapd.conf using the nano text editor. In this file, you define the SSID (WiFi name), channel, and other settings for the rogue AP.

Configuring dnsmasq:
A configuration file named dnsmasq.conf is created to configure the DHCP and DNS settings for the rogue AP.

Routing table and gateway:
Sets up the network interface wlan0mon with a static IP address of 192.168.1.1 and adds a route to the local network.

Internet access sharing:
This section uses iptables to enable internet access sharing for the connected clients via the eth0 interface.

MySQL database setup:
Starts the MySQL service and then uses the mysql command-line tool to create a database named 'fap' and a user named 'fapuser' with specific privileges on the 'fap' database.

Captive portal setup:
Clears the contents of the /var/www/html/ directory, moves the fap.zip file to that directory, and unzips its contents. This sets up a simple web server that can host the captive portal.

Starting the attack:
This section starts the rogue AP using hostapd and configures DNS spoofing using dnsspoof. DNS spoofing is used to redirect DNS requests made by clients to the attacker's IP address (in this case, wlan0mon).

Again, I must emphasize that attempting to execute this script without proper authorization is illegal and unethical. Unauthorized access to networks, data interception, and any form of cyber-attack are serious offenses. Always act responsibly and respect the laws and privacy of others.


## Liability Disclaimer:

The information provided in the script earlier is intended solely for educational and informational purposes. It should not be used for any malicious or unauthorized activities. Engaging in unauthorized network access, cyber-attacks, or any illegal activities is strictly prohibited and can result in severe legal consequences.

The instructions mentioned in the script are designed for understanding various network and security concepts. They should only be used in controlled, legal, and authorized environments with explicit consent from the network owner or administrator.

The misuse of the knowledge presented in this script to create rogue Wi-Fi access points or engage in any form of cyber-attacks is unethical and against the principles of responsible and respectful use of technology.

If you are uncertain about the legality or ethical implications of any action related to networking, security, or any other technology-related matters, seek advice from qualified professionals or authorized personnel.

By accessing and using this information, you agree to act responsibly and lawfully, and you acknowledge that any misuse of this knowledge is solely your responsibility.

Remember, technology can be used to benefit society and improve lives, so let us strive to use our knowledge for positive and ethical purposes.

To the maximum extent permitted by applicable law, I and/or affiliates from whom this repo is sourced and or submitted content to this repo, shall not be liable for any indirect, incidental, special, consequential, or punitive damages, or any loss of profits or revenue, whether incurred directly or indirectly, or any loss of data, use, goodwill, or other intangible losses, resulting from:

👉 (i) your access to this resource and/or inability to access this resource; 
👉 (ii) any conduct or content of any third party referenced by this resource, including, any offensive or illegal conduct or other users or third parties; 
👉 (iii) any content obtained from this resource or any of its resources

