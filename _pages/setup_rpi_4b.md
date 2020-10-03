---
layout: default
title: Setting up Raspberry Pi 4 model B
---

# Setting up Raspberry Pi 4 model B
##### 03-Oct-2020

Setting up my first Raspberry Pi for use - a Raspberry Pi 4 model B - was not too difficult, but it was not trivial either. This is a log of the steps I took to set it up, and some reference documentation. 

At a high level, there are following tasks
* Get NOOBS
* Prepare SD Card for OS installation
* OS installation and first connection
* Secure the SSH server on Raspberry Pi
* Shutdown safely

Let's dive in to details.

### Get NOOBS - New Out Of the Box Software
Download the NOOBS from the [official Raspberry Pi site](https://www.raspberrypi.org/downloads/noobs/). I chose to download the **Offline and network install** image. It is about 2.3 GB in size.

### Prepare SD Card for OS installation
1. Extract NOOBS to the SD card:
   * Format the SD card with FAT32 file system using `fdisk` - detailed instructions [here](http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/)
      * I didn't have to do this, because I was using a fresh bought SD card, which are usually pre-formatted with FAT32 file system
   * Extract the contents of NOOBS to the SD card
      ```
      # use paths per your system
      cd /dev/sdb1
      unzip /path/to/NOOBS.zip
      ```
2. Enable SSH access to the device
   * Create an empty file named `ssh` in the root directory of the SD card - this prompts the OS installer to configure and enable SSH server
3. Configure the device to connect to your wi-fi network
   * Create an empty file named `wpa_supplicant.conf` in the root directory of the SD card, and add following content to it
      ```
      country=IN
      ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
      update_config=1

      network={
      ssid="YOUR_WIFI_SSID"
      scan_ssid=1
      psk="YOUR_WIFI_PASSWORD"
      key_mgmt=WPA-PSK
      }
      ```
4. Configure the installer to execute a silent installation of Raspbian OS
   * Delete all other OSs contained in the `/os` dir so that only Raspbian OS remains
   * Edit the `recovery.cmdline` file in the root NOOBS directory and append `silentinstall` to the arguments list

### OS installation and first connection
1. Now insert the SD card and power on the Raspberry Pi
   * The installer will automatically install the OS
   * Wait for about 10 minutes to let the installation complete
   * Once the installation is complete, the device will automatically connect to the network defined in `wpa_supplicant.conf` file
2. Find the IP address of Raspberry Pi device: 
   * Refer the [official documentation](https://www.raspberrypi.org/documentation/remote-access/ip-address.md)
   * Since [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS) is configured on my router, the hostname `raspberrypi.local` automatically binds to the IP address of the device - just pinging it will tell me the IP address: `ping raspberrypi.local`
3. Connect using SSH - default username / password for Raspberry Pi is `pi` / `raspberry` - [official documentation](https://www.raspberrypi.org/documentation/linux/usage/users.md)
   * Change the default password
   * You might also want to remove the default user and add a new user, in which case, you should also add the new user to sudoer's list

### Secure the SSH server on Raspberry Pi
1. Generate public-private key pair on desktop/laptop
   ```
   ssh-keygen -t rsa -b 4096 -C "Raspberry Pi key"
   ```
2. Upload public key to Raspberry Pi
   ```
   scp ./id_rsa.pub pi@raspberrypi:~/.ssh/authorized_keys
   ```
3. Edit `/etc/ssh/sshd_config` file on Raspberry Pi to change the port number, disable password authentication and enable public key authentication
   ```
   Port 1234
   PermitRootLogin no
   PubkeyAuthentication yes
   PasswordAuthentication no
   PermitEmptyPasswords no
   ```
4. Restart `ssh` service
   ```
   sudo systemctl reload ssh
   ```
5. Now you must connect using private key
   ```
   ssh -i ~/.ssh/id_rsa -p 1234 pi@raspberrypi
   ```

### Clean shutdown
Execute the command `sudo shutdown now` while connected to the device via SSH, and wait for a minute or so, until the green ACT LED stops blinking, leaving the red PWR LED on. Now you can safely turn off the power.

### References
   * [NOOBS Readme: How to Automatically Install an OS](https://github.com/raspberrypi/noobs/blob/master/README.md)
   * [Configuring wpa_supplicant for Raspberry Pi](https://linuxhint.com/rasperberry_pi_wifi_wpa_supplicant/)
      * [Some additional information](https://raspberrypi.stackexchange.com/questions/10251/prepare-sd-card-for-wifi-on-headless-pi)
   * Some interesting discussions about shutting down Raspberry Pi
      * [Safest way to switch off uncleanly](https://raspberrypi.stackexchange.com/questions/28214/safest-way-to-switch-off-uncleanly)
      * [Safe way to shut of Pi without keyboard, access to command line ,etc](https://raspberrypi.stackexchange.com/questions/6914/safe-way-to-shut-of-pi-without-keyboard-access-to-command-line-etc)
      * [How to shut down RPi when running headless](https://raspberrypi.stackexchange.com/questions/4719/how-to-shut-down-rpi-when-running-headless/4722#4722)
   * More offical reference documentation
      * [Raspberry Pi 4 Tech Specs](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/specifications/)
      * [Raspberry Pi 4 Product Brief](https://static.raspberrypi.org/files/product-briefs/200521+Raspberry+Pi+4+Product+Brief.pdf)
      * [Documentation](https://www.raspberrypi.org/documentation/linux/) of some fundamental Linux usage, and commands for getting around the Pi and managing its file system and users.
      * [Basic examples](https://www.raspberrypi.org/documentation/usage/) to help you get started with some of the software available in Raspberry Pi OS
      * [Raspberry Pi 4 Schematics](https://www.raspberrypi.org/documentation/hardware/raspberrypi/schematics/rpi_SCH_4b_4p0_reduced.pdf)
      * [Mechanical Drawings](https://www.raspberrypi.org/documentation/hardware/raspberrypi/mechanical/README.md)
      
