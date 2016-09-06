# Setting Up a Dash Masternode

#### About this guide
This guide will walk you through the process of setting up a [dash masternode](http://dashmasternode.org/) using a __Mac OS X__ local machine and your own remote __Linux__ virtual private server (VPS).  It is adapted from the following guides:
* https://www.dash.org/forum/threads/masternode-setup-guide-using-os-x-local-linux-remote.1776/
* https://www.dash.org/forum/threads/taos-masternode-setup-guide-for-dummies-updated.2680/

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

## 1. Download & install Dash-Qt & prepare your wallet
The following steps will help you [install a dash wallet on your Mac OS X](https://node40.com/2016/02/26/how-to-install-and-secure-the-dash-qt-(core)-wallet.html).  [This video](https://www.youtube.com/watch?v=hCGZPN0Sb84&index=3&list=PLiFMZOlhgsYLWcmb-MT6x7cIxb01OoJTB) may help as well, although it is a bit dated.

1. From a browser on your Mac, go to https://www.dash.org/downloads
2. Find and click the Dash Core, Mac OS X dmg download link
3. Click the downloaded dmg file to open up its contents
4. Drag the Dash-Qt.app file into the Applications folder
5. Open the Applications folder and press control while clicking Dash-Qt
6. From the menu shown, click open, (confirm by clicking open again if needed)
7. Install the app into the default directory
8. Allow it to load and wait for the application to fully sync (progress is shown at bottom)
9. [Encrypt your wallet](https://www.youtube.com/watch?v=PcnAvExGLJs&index=8&list=PLiFMZOlhgsYLWcmb-MT6x7cIxb01OoJTB) and [back it up](https://node40.com/2016/03/30/how-to-backing-up-your-dash-public-key-by-dumping-the-corresponding-private-key.html) (before depositing any dash)

## 2. Create and secure a Linux VPS
1. Create a Ubuntu 64-bit Linux virtual private server (VPS)
  * You may use any service for this, e.g. AWS, Digital Ocean, Vultr, etc
  * You should have secured the necessary ports, created tough logins, etc
  * See [this link](https://github.com/riongull/notes/blob/master/VPS-setup.md) for a step-by-step tutorial using [Vultr](http://www.vultr.com/?ref=6971315-3B)

## 3. If necessary, move dashd to the proper folder
Installing Dash-Qt may have put dashd in your "downloads" folder. If so, we'll need to move the file:

1. Shut down Dash-Qt
2. Open the terminal utility (Applications > Utilities > Terminal)
3. Enter the following commands:

  ```sh
  Local$ cd ~/Library/Application\ Support/Dash
  Local$ ls -la
  # if you don't see a file called dashd, run the following commands
  Local$ cd ~/Downloads
  Local$ mv dashd ~/Library/Application\ Support/Dash
  ```

## 4. FIX THIS SECTION WHEN I KNOW IT'S WORKING Create your masternode key & address, store in separate file
1. Re-open Dash-Qt  
2. Get a new masternode private key and address
  * Menu > Tools > Debug console
  * A new window should appear with the "Console" tab selected at the top
  * Enter the following command at the bottom
  ```sh
  Dash$ masternode genkey
  # Dash will output the result
  Dash$ getaccountaddress 0
  # Dash will output the result
  ```
3. Copy and label the two outputted strings of characters to another application like Word or Notes
  * These will be referred to as \<yourmasternodeprivkey> and \<yourzeroaddress> in step 6.4 below

4. Create a new dash 'zero' address for your masternode
  * File > Receiving addresses > New
  * Label the address (e.g. "MN01"), click "OK", and
  * Leave the 'Receiving addresses' dialog box for the next step
  * Note: you will need a different address for each masternode you plan to create

## 5. Fund your newly created address with 1000 DASH
1. These steps assume you already have >1000 DASH (1000 + miner fee) in your Dash-Qt wallet
2. Open the 'Receiving addresses' dialog box if necessary (file > Receiving addresses)
2. Click the Receiving address you made in step 4 (e.g. "MN01") and click the 'copy' button
3. Click the Send tab on the main Dash-Qt window
4. Paste the address you copied on the 'Pay To' field, it should populate your label
5. Fund your masternode (e.g. MN01) address with *exactly* 1000 DASH
  * You need a small amount extra in the wallet you are sending from in order to cover the miner fee
  * The amount you actually send must be one transaction of exactly 1000 DASH
  * No, you may not send more than 1000 DASH
  * No, you may not send 999.99 DASH
  * No, you may not put in 1 DASH first and then 999 DASH. It must be all at once. You may test the address first, but you will still need to send 1000 DASH later, all in one transaction
  * No, if you have 1000 DASH in the wallet already, that doesn't count. You must send it to yourself by sending it to your new address

## 6. Prepare your remote VPS
While we are waiting for the needed 6 confirmations of our 1000 DASH transaction, we can now prepare the remote server.

1. Log in to your VPS

  ```sh
  Local$ ssh <login-user>@<ip.add.re.ss>
  <password> # if needed
  ```
  * If you changed your SSH port in step 3.5 of [securing your VPS](https://github.com/riongull/notes/blob/master/VPS-setup.md#3-secure-the-vps-using) you may need to:
  ```sh
  Local$ ssh -p <ssh-port-number> <login-user>@<ip.add.re.ss>
  ```
  * You may also log in from your VPS cloud provider's console

2. Optionally, create a new user on your VPS for all dash-related files and functions

  ```sh
  VPS$ su <super-user>
  <password>
  VPS$ sudo adduser <dash-user> # this will be the assumed target for '~' from now on (cd ~ == cd /home/<dash-user>)
  <super-users-password>
  <newPassword>
  <newPassword>
  <otherFieldsAsDesired>
  ```

3. Download, unpack, copy, and permission the needed applications/files on your VPS

  ```sh
  VPS$ su <dash-user> # whatever user you want; <dash-user> if you created it above
  VPS$ cd ~
  VPS$ wget https://www.dash.org/binaries/dash-0.12.0.58-linux64.tar.gz
  VPS$ tar xfvz dash-0.12.0.58-linux64.tar.gz # unpack files
  VPS$ cp dash-0.12.0/bin/dashd dashd
  VPS$ cp dash-0.12.0/bin/dash-cli dash-cli
  VPS$ chmod 755 dashd # set permissions
  ```
4. Create dash.config file on your VPS

  ```sh
  VPS$ mkdir .dash
  VPS$ cd .dash
  VPS$ nano dash.conf
  # once open, insert the following text.  Note: rpcuser and rpcpassword can be anything, you will not have to remember them later, feel free to go nuts on your keyboard

  < # start of file contents
    rpcuser=<anything-like-random-numbers-and-letters>
    rpcpassword=<anything-like-random-numbers-and-letters>
    rpcallowip=127.0.0.1
    listen=1
    server=1
    daemon=1
    logtimestamps=1
    maxconnections=256
    masternode=1
    masternodeprivkey=<yourmasternodeprivkey>
  > # end of file contents, ctrl+x to exit, save as "dash.conf"
  ```
5. Launch dashd on your VPS

  ```sh
  VPS$ cd ~
  VPS$ ./dashd # enter command, then wait ~15 seconds
  VPS$ ./dash-cli getinfo
  ```
  * If you run the "getinfo" command several times you should see that the number of blocks is increasing
  * The number of blocks must eventually catch up to the current blockchain before your masternode is active
  * You can check if the number of blocks is up to the current height by comparing to the current number of blocks reported on one of the many Dash blockchain explorers (several are listed on the dash.org website)
  * You don't need to wait for the blocks to completely sync; we may move on to the next step

## 7. Remove unnecessary files & folders from your VPS
We are done with the installation files and folders, so those can be removed.

1. Remove files as follows:

  ```sh
  VPS$ cd ~
  VPS$ ls
  VPS$ rm -rf dash-0.12.0
  VPS$ rm dash-0.12.0.58-linux64.tar.gz
  VPS$ exit # rion added, check flow
  ```

## 8. Create dash.conf & masternode.conf files on your *local* machine
1. Close Dash-Qt if open
2. Open a terminal session
3. Create dash.conf file

  ```sh
  Local$ cd ~/Library/Application\ Support/Dash
  Local$ nano dash.conf # this should bring up a GNU session that is blank (unless you already had a conf file created). In any case, make sure it has the following text.
  < # start of file contents
    rpcuser=<enter a username of your choosing>
    rpcpassword=<enter a really long string of random characters>
    rpcallowip=127.0.0.1
    listen=0
    server=1
    daemon=1
    logtimestamps=1
    maxconnections=8
  > # end of file contents, ctrl+x to exit, save as "dash.conf"
  ```

4. Obtain data for the masternode.config file
  1. Method 1 (using a block explorer):  
    1. In a block explorer, e.g. [chainz](https://chainz.cryptoid.info/dash/), enter the receiving address for your masternode that you deposited your 1000 DASH into
    2. Find the transaction ID and index of your 1000 DASH deposit
    3. Click on the "hash" of the 1000 DASH transaction you just completed
    4. Find the transaction listed under "outputs" with an index number
    5. Use this hash and index number for your masternode.conf file below
  2. Method 2 (using Dash-Qt):
    1. Click on the transactions tab and double click on the 1000 DASH transaction (it should be the most recent transaction and listed as "Payment to yourself")
    3. Copy the "Transaction ID" without the "-" and three numbers on the far right, and paste that into a block explorer.
    4. Find the address with the 1000 DASH deposit and an index number
    5. Use this hash and index number for your masternode.conf file below
5. Create masternode configuration file

  ```sh
  Local$ nano masternode.conf # this should bring up a new GNU session. You will need to select a name or "alias" for each of your masternodes. In the example below, I have chosen "MN01", but you can name it whatever you want. Populate the file with the data obtained above, as follows:
  < # start of file contents
    MN01 <remote_masternode_IP_Address>:9999 <your_masternode_private_key> <1000_Dash_txn_hash> <deposit_index_number>
  > # end of file contents, exit with ctrl+x, save the file
  ```
  * You will need a separate line for each masternode in the masternode.conf file
  * You may add as many masternodes to the same wallet and the masternode.conf file as you wish
6. Close Dash-Qt

## 9. Start your masternode(s)
1. Launch Dash-Qt
  * This will now use the new settings you just saved in the confguration file in the step above
2. Open a Dash-Qt console session  
3. Enter the following to activate your remote masternode

    ```sh
    Dash$ walletpassphrase <enter passphrase> 60
    Dash$ masternode start-alias <alias of the masternode you are starting>
    ```
  * You should get a message saying "started masternode successfully"
4. Check your work by going back to your remote server and enter the following

    ```sh
    Local$ ssh <login-user>@<ip.add.re.ss>  
    VPS$ ./dash-cli masternode list full | grep <your MN IP address>
    ```
  * If it doesn't show enabled, don't panic; the blockchain must fully download on the remote server before it becomes active
  * You can check the status of the blockchain download by running the "getinfo" command repeatedly until it is fully caught up to the current number of blocks
  * Once it is caught up, give it a minute and try again to see if it shows as "ENABLED"
  * If your address comes up with "ENABLED" in the string, you've done everything correct Congratulations, your masternode is set up correctly, you are done!
