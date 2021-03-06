# Dash Masternode Notes

#### About this guide
This document provides general guidance and a list of popular links related to operating a [dash masternode](http://dashmasternode.org/)

#### Using this guide
* Basic terminal usage
  * This [basic terminal reference page](https://github.com/riongull/notes/blob/master/terminal_notes.md) may help if you are new to using terminal/shell/bash
* Setup assumptions/reference
  * Many dash mastenode operators (MNOs) have set up a split wallet system
  * When working with such a setup, you are generally issuing commands in any one of three locations, as shown in the legend below
  * This [masternode setup guide](https://github.com/riongull/notes/blob/master/dashmasternode_setup.md) may help if you are looking to set up a masternode
* Command prompt legend
  * `Local$ sample command` - a command run on your __local Mac OS X__ terminal
  * `VPS$ sample command` - a command run on your __remote virtual private server's__ terminal
  * `Dash$ sample command` - a command run on your __local Dash-Qt's__ console
* Running from Dash-Qt vs VPS
  * Full commands are not shown in all sections; keep the follwoing in mind:
    * When running commands your VPS, you must be in the proper directory and preface commands with `./dash-cli`
    * When running from Dash-Qt there is no need to call `./dash-cli`

## Starting your masternode(s)
1. Launch Dash-Qt
2. Open a Dash-Qt console session (Tools > Debug console)
3. Enter the following:

    ```sh
    Dash$ walletpassphrase <your-wallet-passphrase> 60 # this unlocks your wallet, the passphrase is the same one you created to encrypt your wallet
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
2. `VPS$ cd ~` (or whatever directory holds dash-cli and dashd)
3. `VPS$ ./dash-cli stop`


## Checking your masternode's place in payment queue

## All Dash-cli commands
Commands in the following subsections should be issued with the following format:
```sh
VPS$ ./dash-cli "command-listed" <plus-other-fields> ( as-shown )
```
where:
* items in `"quotes"` are commands or values you provide,
* items in `<angle brackets>` are arguments/values you provide,
* items `<separated|by|pipes>` are mutually exclustive options, and
* Itmes in `( parenthases )` are optional
* *Note: this help documentation can also be found by running `VPS:$ ./dash-cli help` from the directory containing `dash-cli` and `dashd` while `dashd` is running*

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
```sh
getinfo
help ( "command" )
stop
```

#### Dash
```sh
darksend <dashaddress> <amount>
masternode "command"... ( "passphrase" )
masternodelist ( "mode" "filter" )
mnbudget "command"... ( "passphrase" )
mnbudgetvoteraw <masternode-tx-hash> <masternode-tx-index> <proposal-hash> <yes|no> <time> <vote-sig>
mnfinalbudget "command"... ( "passphrase" )
mnsync [status|reset]
spork <name> [<value>]
```

##### masternode "command" options
* found by typing `VPS$ ./dash-cli help masternode`

```sh
masternode "command"... ( "passphrase" )
```

Set of commands to execute masternode related actions

Arguments:
* "`command`"        (string or set of strings, required) The command to execute
* "`passphrase`"     (string, optional) The wallet passphrase

Available `command`s:
```sh
count             # Print number of all known masternodes (optional: 'ds', 'enabled', 'all', 'qualify')
current           # Print info on current masternode winner
debug             # Print masternode status
genkey            # Generate new masternodeprivkey
enforce           # Enforce masternode payments
outputs           # Print masternode compatible outputs
start             # Start masternode configured in dash.conf
start-alias       # Start single masternode by assigned alias configured in masternode.conf
start-<mode>      # Start masternodes configured in masternode.conf (<mode>: 'all', 'missing', 'disabled')
status            # Print masternode status information
list              # Print list of all known masternodes (see masternodelist for more info)
list-conf         # Print masternode.conf in JSON format
winners           # Print list of masternode winners
```

##### masternodelist "mode" options
* found by typing `VPS$ ./dash-cli help masternodelist`
```sh
masternodelist ( "mode" "filter" )
```

Arguments:
* "`mode`"      (string, optional/required to use filter, defaults = status) The mode to run list in
* "`filter`"    (string, optional) Filter results. Partial match by IP by default in all modes, additional matches in some modes are also available

Available `mode`s:
```sh
activeseconds     # Print number of seconds masternode recognized by the network as enabled (since latest issued `masternode start/start-many/start-alias`)
addr              # Print ip address associated with a masternode (can be additionally filtered, partial match)
full              # Print info in format `status` `protocol` `pubkey` `IP` `lastseen` `activeseconds` `lastpaid` (can be additionally filtered, partial match)
lastseen          # Print timestamp of when a masternode was last seen on the network
lastpaid          # The last time a node was paid on the network
protocol          # Print protocol of a masternode (can be additionally filtered, exact match))
pubkey            # Print public key associated with a masternode (can be additionally filtered partial match)
rank              # Print rank of a masternode based on current block
status            # Print masternode status: ENABLED / EXPIRED / VIN_SPENT / REMOVE / POS_ERROR (can be additionally filtered, partial match)
```

##### mnbudget "command" options
* found by typing `VPS$ ./dash-cli help mnbudget`
```sh
mnbudget "command"... ( "passphrase" )
```

Vote or show current budgets

Available `command`s:
```sh
prepare            # Prepare proposal for network by signing and creating tx
submit             # Submit proposal for network
vote-many          # Vote on a Dash initiative
vote-alias         # Vote on a Dash initiative
vote               # Vote on a Dash initiative/budget
getvotes           # Show current masternode budgets  (DEPRECATED?)
getinfo            # Show current masternode budgets
show               # Show all budgets
projection         # Show the projection of which proposals will be paid the next cycle
check              # Scan proposals and remove invalid
nextblock          # Get next superblock for budget system
```

#### Generating
```sh
getgenerate
gethashespersec
setgenerate generate ( genproclimit )
```

#### Mining
```sh
getblocktemplate ( "jsonrequestobject" )
getmininginfo
getnetworkhashps ( blocks height )
prioritisetransaction <txid> <priority delta> <fee delta>
submitblock "hexdata" ( "jsonparametersobject" )
```

#### Network
```sh
addnode "node" "add|remove|onetry"
getaddednodeinfo dns ( "node" )
getconnectioncount
getnettotals
getnetworkinfo
getpeerinfo
ping
```

#### Rawtransactions
```sh
createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,...}
decoderawtransaction "hexstring"
decodescript "hex"
getrawtransaction "txid" ( verbose )
sendrawtransaction "hexstring" ( allowhighfees )
signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )
```

#### Util
```sh
createmultisig nrequired ["key",...]
estimatefee nblocks
estimatepriority nblocks
validateaddress "dashaddress"
verifymessage "dashaddress" "signature" "message"
```

#### Wallet
```sh
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
