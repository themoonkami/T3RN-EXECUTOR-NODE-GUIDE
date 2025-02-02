# T3RN-EXECUTOR-NODE-GUIDE

As with running all nodes, i would recommend you purchase a VPS for running the t3rn executor node. You can purchase a suitable package from contabo (https://contabo.com/en/vps/)


Now, to setting up the node itself:

In your device terminal, run the following commands to create and navigate to a t3rn directory

To create:  
```
mkdir t3rn
```
To navigate:  
```
cd t3rn
```
 
Download the latest release by copying and pasting this:  
For Ubuntu: 
```
curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | \
grep -o '"tag_name": "[^"]*' | \
cut -d'"' -f4 | \
xargs -I {} curl -LO https://github.com/t3rn/executor-release/releases/download/{}/executor-macos-{}.tar.gz
```
For MacOS:  
```
curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | \
grep -o '"tag_name": "[^"]*' | \
cut -d'"' -f4 | \
xargs -I {} curl -LO https://github.com/t3rn/executor-release/releases/download/{}/executor-macos-{}.tar.gz
```


Extract the archive:  
For Ubuntu:  
```
tar -xzf executor-linux-*.tar.gz
```
For MacOS
```
tar -xzf executor-macos-*.tar.gz
```

Configuring settings and environment  
1) Setup your node environment
```
export NODE_ENV=testnet
```
2) Configure log settings
```
export LOG_LEVEL=debug
export LOG_PRETTY=false
```
This determines how and what information the logs will display  

3) Processing Bids, Orders and Claims
```
export EXECUTOR_PROCESS_BIDS_ENABLED=true
export EXECUTOR_PROCESS_ORDERS_ENABLED=true
export EXECUTOR_PROCESS_CLAIMS_ENABLED=true
```
Setting the values to true enables an executor to process bids, orders and claims. Setting them to false will stop the executor from picking up new bids, orders and claims.  

4) Specifying maximum gas usage.
```
export EXECUTOR_MAX_L3_GAS_PRICE=1000
```
This means that if gwei goes above 1000, your node will not process orders until it falls below that amount. Personally, mine is set at 10000 to allow me process transactions even when gwei is high.  
Remember, the higher the gwei, the more eth is deducted from your balance.  

PRIVATE KEY

The PRIVATE_KEY_LOCAL variable of your executor should be the private key of the wallet you plan to run the node with. Copy the coomand below and replace "YOUR_PRIVATE_KEY" with the actual private key of your EVM wallet.
```
export PRIVATE_KEY_LOCAL=YOUR_PRIVATE_KEY
```
NETWORKS & RPC

You need to enable your node to execute orders across 4 networks: arbitrum, optimism, base and blast
