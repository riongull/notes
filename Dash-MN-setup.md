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
1. From a browser on your Mac, go to https://www.dash.org/downloads
2. Find the latest Mac OS X Dash-Qt wallet and click the download link
3. Double click the downloaded dmg file to install it locally
4. Drag the contents to your application folder
5. Open Dash-Qt and allow it to fully sync
6. Encrypt your wallet and back it up (before depositing any dash)

## 2. Create and secure a Linux VPS
1. Create a Ubuntu 64-bit Linux virtual private server (VPS)
  * You may use any service for this, e.g. AWS, Digital Ocean, Vultr, etc
  * You should have secured the necessary ports, created tough logins, etc
  * See [this link](https://github.com/riongull/notes/blob/master/VPS-setup.md) for a step-by-step tutorial using [Vultr](http://www.vultr.com/?ref=6971315-3B)

## 3. If necessary, move dashd to the proper folder
Installing Dash-Qt may store dashd in your "downloads" folder. If so, move the file as follows:

&nbsp;1\. Shut down Dash-Qt  
&nbsp;2\. Open the terminal utility (Applications > Utilities > Terminal)  
&nbsp;3\. Enter the following commands:  
```sh
Local$ cd ~
Local$ cd ~/Downloads
Local$ mv dashd ~/Library/Application\ Support/Dash
```    
## 4. Create your masternode key & address, store in separate file
&nbsp;1\. Re-open Dash-Qt  
&nbsp;2\. Get a new address and masternode private key  
  * Menu > Tools > Debug console
  * A new window should appear with the "Console" tab selected at the top
  * Enter the following command at the bottom
  ```sh
  Dash$ masternode genkey
  ```
&nbsp;3\. Copy the string of characters to another application like Word or Notes (you will need that string later)
&nbsp;4\. Create a new dash address for your masternode
  * File > Receiving addresses > New
  * Label the address (e.g. "MN01")
  * You will need a different address for each masternode you plan to create

## 5. Fund your newly created address with 1000 DASH
1. Fund your the address just created with 1000 DASH
  * It must be one transaction of exactly 1000 DASH
  * No, you may not send more than 1000 DASH
  * No, you may not send 999.99 DASH
  * No, you may not put in 1 DASH first and then 999 DASH. It must be all at once. You may test the address first, but you will still need to send 1000 DASH later, all in one transaction
  * No, if you have 1000 DASH in the wallet already, that doesn't count. You must send it to yourself by sending it to your new address

## 6. Prepare your remote VPS
While we are waiting for the needed 6 confirmations of our 1000 DASH transaction, we can now prepare the remote server.

&nbsp;1\. Log in to your VPS

```sh
Local$ ssh <normal-user≥@<ip.add.re.ss>
```
  * If you did not set up SSH when you [secured up your VPS](https://github.com/riongull/notes/blob/master/VPS-setup.md#3-secure-the-vps-using) you will need to enter the password for ```<normal-user>```
  * You may also log in from your VPS cloud provider's console

&nbsp;2\. Download, unpack, copy, and permission the needed applications/files on your VPS

```sh
VPS$ cd ~
VPS$ wget https://www.dash.org/binaries/dash-0.12.0.58-linux64.tar.gz
VPS$ tar xfvz dash-0.12.0.58-linux64.tar.gz # unpack files
VPS$ cp dash-0.12.0/bin/dashd dashd
VPS$ cp dash-0.12.0/bin/dash-cli dash-cli
VPS$ chmod 755 dashd # set permissions
```
&nbsp;3\. Create dash.config file on your VPS

```sh
VPS$ mkdir .dash
VPS$ cd .dash
VPS$ nano dash.conf
# once open, insert the following text
< # start of file contents
  rpcuser=<enter any user name>
  rpcpassword=<enter any long password>
  rpcallowip=127.0.0.1
  listen=1
  server=1
  daemon=1
  logtimestamps=1
  maxconnections=256
  masternode=1
  masternodeprivkey=<enter your masternode key which you generated earlier>
> # end of file contents, ctrl+x to exit, save as "dash.conf"
```
&nbsp;4\. Launch dashd on your VPS

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

&nbsp;4\. Obtain data for the masternode.config file
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
&nbsp;5\. Create masternode configuration file

```sh
Local$ nano masternode.conf # this should bring up a new GNU session. You will need to select a name or "alias" for each of your masternodes. In the example below, I have chosen "MN01", but you can name it whatever you want. Populate the file with the data obtained above, as follows:
< # start of file contents
  MN01 <remote_masternode_IP_Address>:9999 <your_masternode_private_key> <1000_Dash_txn_hash> <deposit_index_number>
> # end of file contents, exit with ctrl+x, save the file
```
  * You will need a separate line for each masternode in the masternode.conf file
  * You may add as many masternodes to the same wallet and the masternode.conf file as you wish
&nbsp;6\. Close Dash-Qt

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
Local$ ssh <normal-user≥@<ip.add.re.ss>  
VPS$ ./dash-cli masternode list full | grep <your MN IP address>
```
  * If it doesn't show enabled, don't panic; the blockchain must fully download on the remote server before it becomes active
  * You can check the status of the blockchain download by running the "getinfo" command repeatedly until it is fully caught up to the current number of blocks
  * Once it is caught up, give it a minute and try again to see if it shows as "ENABLED"
  * If your address comes up with "ENABLED" in the string, you've done everything correct Congratulations, your masternode is set up correctly, you are done!
