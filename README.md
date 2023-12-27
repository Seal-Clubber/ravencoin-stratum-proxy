# aipg-stratum-proxy
Allows you to mine directly to your own local wallet/node with any mining software that uses the stratum protocol.

If you are a windows user and are not familiar with python, a walk-through and auto installer is avaliable for a (hopefully) easy install. See [here](#windows).

## *Important Note 1*
This is not pool software and is meant for solo-mining. All proceeds go to the address of the first miner that connects.

## *Important Note 2*
Mining software will only send a share when it has found a block. No shares for long periods of time is normal behavior.

## Table of Contents  
- [Setup](#setup)
- [Node Requirements](#node)
- [Usage](#usage)
- [Help](#help)

<a name="setup"/>

## Setup:

1. Requires python 3.8+
2. Run `python3 -m pip install -r requirements.txt`
  - Note that the pysha3 module will need to be compiled so you need some kind of C compiler installed. Alternatively, a precompiled `.whl` is avaliable in `windows/python_modules`.

<a name="windows"/>

#### For Windows:
A bat file is avaliable to auto install python and dependencies and generate another bat file to run the stratum.
1. Ensure your node is configured [as required](#node).
2. (Re)start your node (the qt wallet works).
3. Download this repo (https://github.com/AIPowerGrid/aipg-stratum-proxy/archive/refs/heads/master.zip)
4. Unzip the downloaded file
5. Open the unzipped folder
6. Open the `windows` folder
7. Double-click `generate_bat.bat`
8. After `generate_bat.bat` completes with no errors, go back to the previous folder.
9. Double-click `run.bat` to run the stratum converter.

<a name="node"/>

## Node Requirements:

Requires the following `aipg.conf` options:
```
server=1
rpcuser=my_username
rpcpassword=my_password
rpcallowip=127.0.0.1
```
On *nix OS's this file is located at `~/.aipg` by default. On windows, this file is located at `%appdata%\roaming\Aipg`.

You may need to create the `aipg.conf` file and add those lines if it does not exist.

For testnet you can add `testnet=1` to your `aipg.conf`

note:
- Default Mainnet rpcport = `9788`
- Default Testnet rpcport = `19788`

Make sure you configure the rpcport on `stratum-converter.py` accordingly.

<a name="usage"/>

## Usage:
The stratum converter uses the following flags `python stratum-converter.py Port_for_miner Ip_of_node Rpc_username Rpc_password Rpc_port Allow_external_connections Is_testnet(optional)` 

With this in mind we can run **testnet** from a local node with a local miner:
```
python3 stratum-converter.py 54325 localhost my_username my_password 18766 false true
```
And for a local node on **mainnet** with an external miner:
```
python3 stratum-converter.py 54325 localhost my_username my_password 8766 true
```

Connect to it with your miner of choise:

| status | miner | example |
| - | - | - |
| :heavy_check_mark: Works | T-rex | t-rex -a kawpow -o stratum+tcp://PROXY_IP:54325 -u YOUR_WALLET_ADDRESS -p x |
| :heavy_check_mark: Works | TeamRedMiner | teamredminer -o stratum+tcp://PROXY_IP:54325 -u YOUR_WALLET_ADDRESS -p x --eth_hash_report=on |
| :heavy_check_mark: Works | Gminer | miner --algo kawpow --server stratum+tcp://PROXY_IP:54325 --user YOUR_WALLET_ADDRESS --pass x |
| :exclamation:   Errors | NBminer | :grey_question: |
| :heavy_check_mark: Works | kawpowminer | kawpowminer -P stratum+tcp://YOUR_WALLET_ADDRESS.worker@PROXY_IP:54325 |

<a name="help"/>

## Help:
@sealclubber is avaliable on the community AIPG server (https://discord.gg/vZ9XrTSRYr)
Donate: 
  - AIPG: Ab8Wn5u6pc29ZhQkk1ocacFn3Hs6mdAioN

Or help support the AIPG team,
Donate: 
  - AIPG: Ab8KBCTTJgy7XnsPsHbnwRMJD4MFjG12hU

@kralverde#0550 is avaliable on the community RVN server (https://discord.gg/jn6uhur)
Donate: 
  - RVN: RMriWfETGV97hskqH8TvSWVZb9idK6fkU6
  - BTC: bc1q9vs8ttd6sg8dvhwwqh5g6c5wjm0fwkfmq2lgff
