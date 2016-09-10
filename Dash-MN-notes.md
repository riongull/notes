# Dash Masternode Notes

#### About this guide
This document provides general guidance and a list of popular links related to operating a dash masternode](http://dashmasternode.org/)

#### Using this guide
* Command promt legend
  * this guide uses the command prompts below to indicate which machine you are running commands on:
  * ```Local$ sample command ``` - run on your __local Mac OS X__ terminal
  * ```VPS$ sample command``` - run on your __remote virtual private server's__ terminal
  * ```Dash$ sample command``` - run on your __local Dash-Qt's__ console
* Command line syntax
  * the text before the ```$``` will look different on your machines
  * simply type what's *after* the ```$``` (and hit enter/return) to execute a given command
  * for a ```$ command -with <text-in-brackets>``` replace ```<text-in-brackets>``` with *your* data (omitting ```<``` and ```>```)

## Starting your masternode(s)
1. Launch Dash-Qt
2. Open a Dash-Qt console session (Tools > Debug console)
3. Enter the following:

    ```sh
    Dash$ walletpassphrase <your-wallet-passphrase> 60 # this is the same password you created to encrypt your wallet
    Dash$ masternode start-alias <alias-of-masternode-you-want-to-start>
    ```
  * You should get a response similar to:

    ```sh
    {
    "alias" : "MN01",
    "result" : "successful"
    }
    ```

## Stopping your masternode(s)
1. Log into your VPS
2. ```VPS$ cd ~``` (or whatever directory holds dash-cli and dashd)
3. ```VPS$ ./dash-cli stop```


## Dash-cli commands
Running ```VPS:~$ ./dash-cli help``` from the directory containing ```dash-cli``` while ```dashd``` produces the following help file commands:

* itmes in `( parenthases )` are optional
* items in `"quotes"` are values you provide
* items in ```<angle brackets>``` are arguments/values you provide
* items ```<separated|by|pipes>``` are mutually exclustive options (choose one)

#### Blockchain
```sh
getbestblockhash
getblock "hash" ( verbose )
getblockchaininfo
getblockcount
getblockhash index
getblockheader "hash" ( verbose )
getchaintips
getdifficulty
getmempoolinfo
getrawmempool ( verbose )
gettxout "txid" n ( includemempool )
gettxoutsetinfo
verifychain ( checklevel numblocks )
```

#### Control
```
getinfo
help ( "command" )
stop
```

#### Dash
```
darksend <dashaddress> <amount>
masternode "command"... ( "passphrase" )
masternodelist ( "mode" "filter" )
mnbudget "command"... ( "passphrase" )
mnbudgetvoteraw <masternode-tx-hash> <masternode-tx-index> <proposal-hash> <yes|no> <time> <vote-sig>
mnfinalbudget "command"... ( "passphrase" )
mnsync [status|reset]
spork <name> [<value>]
```

###### `masternode` "command" options
* found by typing `./dash-cli help masternode` ...

```sh
masternode "command"... ( "passphrase" )
```

Set of commands to execute masternode related actions

Arguments:
* "command"        (string or set of strings, required) The command to execute
* "passphrase"     (string, optional) The wallet passphrase

Available commands:
```sh
count        # Print number of all known masternodes (optional: 'ds', 'enabled', 'all', 'qualify')
current      # Print info on current masternode winner
debug        # Print masternode status
genkey       # Generate new masternodeprivkey
enforce      # Enforce masternode payments
outputs      # Print masternode compatible outputs
start        # Start masternode configured in dash.conf
start#alias  # Start single masternode by assigned alias configured in masternode.conf
start#<mode> # Start masternodes configured in masternode.conf (<mode>: 'all', 'missing', 'disabled')
status       # Print masternode status information
list         # Print list of all known masternodes (see masternodelist for more info)
list-conf    # Print masternode.conf in JSON format
winners      # Print list of masternode winners
```

```
masternode
```

###### ```mnbudget``` "command" options
```
mnbudget
```

#### Generating
```
getgenerate
gethashespersec
setgenerate generate ( genproclimit )
```

#### Mining
```
getblocktemplate ( "jsonrequestobject" )
getmininginfo
getnetworkhashps ( blocks height )
prioritisetransaction <txid> <priority delta> <fee delta>
submitblock "hexdata" ( "jsonparametersobject" )
```

#### Network
```
addnode "node" "add|remove|onetry"
getaddednodeinfo dns ( "node" )
getconnectioncount
getnettotals
getnetworkinfo
getpeerinfo
ping
```

#### Rawtransactions
```
createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,...}
decoderawtransaction "hexstring"
decodescript "hex"
getrawtransaction "txid" ( verbose )
sendrawtransaction "hexstring" ( allowhighfees )
signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )
```

#### Util
```
createmultisig nrequired ["key",...]
estimatefee nblocks
estimatepriority nblocks
validateaddress "dashaddress"
verifymessage "dashaddress" "signature" "message"
```

#### Wallet
```
addmultisigaddress nrequired ["key",...] ( "account" )
backupwallet "destination"
dumpprivkey "dashaddress"
dumpwallet "filename"
encryptwallet "passphrase"
getaccount "dashaddress"
getaccountaddress "account"
getaddressesbyaccount "account"
getbalance ( "account" minconf includeWatchonly )
getnewaddress ( "account" )
getrawchangeaddress
getreceivedbyaccount "account" ( minconf )
getreceivedbyaddress "dashaddress" ( minconf )
gettransaction "txid" ( includeWatchonly )
getunconfirmedbalance
getwalletinfo
importaddress "address" ( "label" rescan )
importprivkey "dashprivkey" ( "label" rescan )
importwallet "filename"
keepass <genkey|init|setpassphrase>
keypoolrefill ( newsize )
listaccounts ( minconf includeWatchonly)
listaddressgroupings
listlockunspent
listreceivedbyaccount ( minconf includeempty includeWatchonly)
listreceivedbyaddress ( minconf includeempty includeWatchonly)
listsinceblock ( "blockhash" target-confirmations includeWatchonly)
listtransactions ( "account" count from includeWatchonly)
listunspent ( minconf maxconf  ["address",...] )
lockunspent unlock [{"txid":"txid","vout":n},...]
move "fromaccount" "toaccount" amount ( minconf "comment" )
sendfrom "fromaccount" "todashaddress" amount ( minconf "comment" "comment-to" )
sendmany "fromaccount" {"address":amount,...} ( minconf "comment" )
sendtoaddress "dashaddress" amount ( "comment" "comment-to" )
sendtoaddressix "dashaddress" amount ( "comment" "comment-to" )
setaccount "dashaddress" "account"
settxfee amount
signmessage "dashaddress" "message"
```
