# Setting Up a Secure Virtual Private Server (VPS)

#### About this guide
This guide will walk you through the process of setting up a __Linux__-based virtual private server (VPS).  It assumes you are using a __Mac OS X__ local machine.  It is adapted from the following guides:
* http://planetcrypton.com/hardened-server
* https://www.youtube.com/watch?v=DbPDraCYju8
* https://gist.github.com/learncodeacademy/5850f394342a5bfdbfa4

#### Using this guide
* Command promt legend
  * this guide uses the command prompts below to indicate which machine you are running commands on:
  * ```Local$ sample command ``` - run on your __local Mac OS X__ terminal
  * ```VPS$ sample command``` - run on your __remote virtual private server's__ terminal
  * ```Dash$ sample command``` - run on your __local Dash-Qt's__ console
* Command line syntax
  * the text before the ```$``` will look different on your machines
  * simply type what's *after* the ```$``` (and hit enter/return) to execute a given command
  * for a ```$ command -with <text_in_brackets>``` replace ```<text_in_brackets>``` with *your* data (omitting ```<``` and ```>```)

## 1. Create a Linux virtual private server (VPS)

1. Create a [Vultr account](http://www.vultr.com/?ref=6971315-3B)
2. After signing in to Vultr, deploy a new instance
  * Location: somewhere near you
  * Server Type: 64 bit OS > Ubuntu > 14.04 x64
  * Server Size: Memory is the bottleneck for a Masternode, choose 1GB RAM to be safe
3. Click 'Deploy'
4. Wait for your new server to get to 'running' status

## 2. Set up the VPS with new users

1. Log into the *remote* (newly created) VPS from your *local* computer's terminal

  ```sh
  Local$ ssh root@<ip.add.re.ss>
  <defaultPassword>
  ```
2. Change the 'root' user's password

  ```sh
  VPS$ passwd root
  <newPassword>
  <newPassword>
  ```
3. Create a couple new users, give one sudo privileges  

  ```sh
  VPS$ adduser <super-user>
  VPS$ sudo usermod -a -G sudo <super-user> # adds super-user to 'sudo' group
  VPS$ adduser <normal-user>
  ```

## 3. Secure the VPS using...

*... either __passwords__ for logging in to the VPS, by doing the following:*

1. Create strong passwords for ALL users

  ```sh
  # 1.1 give normal-user a secure password
  VPS$ su <normal-user>
  VPS$ passwd
  <newPassword>
  <newPassword>
  VPS$ exit
  # 1.2 give super-user a secure password
  VPS$ su <super-user>
  VPS$ passwd
  <newPassword>
  <newPassword>
  VPS$ exit
  # 1.3 give root a secure password
  VPS$ passwd
  <newPassword>
  <newPassword>
  VPS$ exit
  ```

*...or __SSH__ for logging in to the VPS, by doing the following:*

1. Create SSH folder if needed

  ```sh
  Local$ cd ~
  Local$ ls
  # if there's a folder named .ssh, then skip the next step, otherwise:
  Local$ mkdir ~/.ssh
  ```
2. Create SSH keys

  ```sh
  Local$ touch /home/<your-local-user-name>/.ssh/<dash-server-key> # <dash-server-key> is a descriptive name you are coming up with now, <your-local-user-name> already exists on your computer
  Local$ ssh-keygen -t rsa
  </home/<your-local-user-name>/.ssh/dash-server-key> # replace default path with one we just created
  <really-long-and-hard-to-guess-passphrase>
   # set key permissions
  Local$ chmod 644 /home/<your-LOCAL-user-name>/.ssh/<darkcoin-server-key>.pub
  Local$ chmod 600 /home/<your-LOCAL-user-name>/.ssh/<darkcoin-server-key>
  ```
3. Create/Edit ~/.ssh/config file to handle multiple keys

  ```sh
  Local$ touch ~/.ssh/config
  Local$ chmod 644 ~/.ssh/config
  Local$ nano ~/.ssh/config
  < # Start of contents of new config file
    Host <ip.add.re.ss>
    Hostname <ip.add.re.ss>
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/<dash-server-key>
  > # End of contents of new config file, save and close
  ```
4. Copy/paste the public key from *local* to *remote* and set permissions

  ```sh
  Local$ cd ~/.ssh
  Local$ cat dash-server-key.pub | pbcopy # was id_rsa.pub
  Local$ ssh root@<ip.add.re.ss> #log into VPS
  <password>
  # You're now in your VPS...
  VPS$ mkdir /home/<normal-user>/.ssh/
  VPS$ touch /home/<normal-user>/.ssh/authorized_keys
  VPS$ nano /home/<normal-user>/.ssh/authorized_keys
  [ctrl+x] # press ctrl+x to paste in the key you copied from local
  # Set the permissions.
  VPS$ chown -R <login-user>:<login-user> /home/<login-user>/.ssh
  VPS$ chmod 700 /home/<login-user>/.ssh
  VPS$ chmod 600 /home/<login-user>/.ssh/authorized_keys
  VPS$ exit
  ```
5. Configure SSH on *remote* server

  ```sh
  VPS$ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config_original # copy config file just in case we screw things up while editing it, just in case.
  VPS$ sudo nano /etc/ssh/sshd_config # open the ssh configuration file. The things  we need to check, set, or add within the sshd_config file are below:
  < #start
    Protocol 2
    PermitRootLogin no
    PasswordAuthentication no
    UseDNS no
    AllowUsers <login-user>
  > # end
  VPS$ service ssh restart # restart ssh.  Note that this is a very “strict” configuration.  You will now ONLY be allowed to log-in to your REMOTE server from your current LOCAL machine.  To be able to log-in from a different LOCAL machine you would need to copy the private ssh key from your LOCAL machine onto the other LOCAL machine.  (You might want to keep the private key on an encrypted usb flash drive for such purposes.)  If that other LOCAL machine were not also owned by you, then you would want to delete the private key from it after you were done using it.  If you were willing to compromise just a bit on security you could leave PasswordAuthentication set to yes; it would be better if you could avoid doing this, however, in the event someone guessed or otherwise found out login-user's password.  You should now try to log-out as root and then ssh log-in as <login-user>:
  VPS$ exit
  Local$ ssh <login-user>@<ip.add.re.ss>
  <password> # if you can successfully log-in at this point, then you can continue on to the “Configuring Ports” section below.  If you cannot log-in, then you can try to go back and fix any problems by logging-in through a web-based console provided by your cloud-server's host.  If you just can't get it working no matter what, you may have to start again, rebuilding the server from scratch.
  ```

## 4. Configure VPS ports

1. Configure default access

  ```sh
  VPS$ su <general-user>
  # deny all incoming and allow all outgoing connections by default:
  VPS$ sudo ufw default deny incoming
  VPS$ sudo ufw default allow outgoing
  ```

2. Edit SSH port for TCP connections

  ```sh
  # for security, you will want to change ssh-port-number for tcp connections, and open that port.  (We will refer to this as <ssh-port-number>.)
  VPS$ sudo ufw allow <ssh-port-number>/tcp
  ```

3. Configure desired ports (common ports shown)

  ```sh
  # you may now open a number of commonly used ports. You may not need some of these ports, or be unsure as to which you do or do not need.  For most configurations, opening the ports shown below should be safe.  If you are sure that you do not need to open some port, feel free to skip that step.  Also if you wanted to close a port later on, you could to this by simply issuing the command: sudo ufw deny <port>/<optional: protocol>.  For example, to close port 53 for everything: sudo ufw deny 53. To deny incoming tcp packets to port 53: VPS$ sudo ufw deny 53/tcp. To deny incoming udp packets to port 53: VPS$ sudo ufw deny 53/udp.  
  # commands to open commonly used ports/protocols:
  VPS$ sudo ufw allow 25/tcp # SMTP - Simple Mail Tranfer Protocol Transmission
  VPS$ sudo ufw allow 53/tcp # DNS - Dynamic Name Server (use both lines)
  VPS$ sudo ufw allow 53/udp
  VPS$ sudo ufw allow 80/tcp # HTTP - Hyper-Text Transfer Protocol
  VPS$ sudo ufw allow 110/tcp # POP3 - Post Office Protocol
  VPS$ sudo ufw allow 143/tcp # IMAP - Internet Mail Access Protocol
  VPS$ sudo ufw allow 443/tcp # HTTPS - Hyper-text Tranfer Protocol Secure
  VPS$ sudo ufw allow 465/tcp # SMTPS - Simple Mail Tranfer Protocol Secure
  VPS$ sudo ufw allow 587/tcp # SMTP - Simple Mail Tranfer Protocol Submission
  # commands to open commonly used ports/protocols related to Dash
  VPS$ sudo ufw allow 7903 # P2Pool-dash, needed if you are running a Dash P2Pool
  VPS$ sudo ufw allow 9999/tcp # Dash port 9999:mainnet, needed if you are running Dash on the standard main network, both lines
  VPS$ sudo ufw allow 9999/udp
  VPS$ sudo ufw allow 19999/tcp # Darkcoin Port 19999:testnet, needed if you are running Dash on the testing network, both lines
  VPS$ sudo ufw allow 19999/udp
  ```

4. Re-edit SSH confguration file

  ```sh
  # edit the ssh configuration file again, just to change the Port to the <ssh-port-number> you chose above:
  VPS$ sudo nano /etc/ssh/sshd_config
  < # just change the one line:
    Port <ssh-port-number>
  >
  ```

5. Enable UFW, reboot VPS, log back in from Local

  ```sh
  VPS$ sudo ufw enable # enable UFW.
  VPS$ sudo ufw status numbered # check its status (you can omit the word “numbered,” but it provides more information)
  VPS$ sudo reboot # reboot the server,
  # you should now be able to log back in using our ssh private key and ssh passphrase, now also including the new <ssh-port-number> in the login. You may have to wait about a minute or so for it to boot up before you can login
  Local$ ssh -p <ssh-port-number> <login-user>@<ip.add.re.ss> # log back in, if it works, continue to the next section, “Update and Upgrade and Install General-Dependencies.”  If it does not work, you may have to rebuild from scratch, unless you can log-in via a web-console provided by your cloudserver host to try to fix the problem.
  ```

## 5. Update, upgrade, & install general VPS dependencies

1. Switch to super-user, and super-user's home directory and update the package list

  ```sh
  VPS$ su <super-user>
  VPS$ cd ~
  VPS$ sudo apt-get update
  VPS$ sudo apt-get upgrade
  VPS$ sudo apt-get dist-upgrade
  ```

2. Install general dependencies/packages, reboot, and log back in

  ```sh
  VPS$ sudo aptitude install git build-essential screen curl mailutils
  VPS$ sudo reboot # as before, you may have to wait a very short time for it to boot up before you can login.)
  VPS$ ssh -p <ssh-port-number> <login-user>@<ip.add.re.ss>
  VPS$ su <general-user>
  VPS$ cd ~
  ```

You're done setting up your secure, "hardened" Linux server!
