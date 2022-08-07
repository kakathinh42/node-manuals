# Challenge 004

## Monitor and make alerts

An email notification can make it more comfortable to maintain a validator up and running. Achieve to be a validator confirming transactions on testnet and get >95% of uptime.

## Log Files

The log file is stored either in the ~/.nearup/logs directory or in systemd depending on your setup.

### Systemd Command

```
journalctl -n 100 -f -u neard | ccze -A
```
![Neard Log](../challenges/images/log%20service%20near.png)

### Log sample
```
INFO stats: # 1823230 3EcvGFnq1du6SuhiXw3jSUb1ALbVBCSVV9hsmXUJYKy6 Validator | 100 validators 30 peers ⬇ 1.62 MB/s ⬆ 1.76 MB/s 0.40 bps 848 Tgas/s CPU: 161%, Mem: 6.93 GB
```
* Validator: A “Validator” will indicate you are an active validator
* 100 validators: Total 100 validators on the network
* 30 peers: You current have 30 peers. You need at least 3 peers to reach consensus and start validating
* #46199418: block — Look to ensure blocks are moving

### Install RPC

```
sudo apt install curl jq
```
### Check your node version
```
curl -s http://127.0.0.1:3030/status | jq .version
```
![version](../challenges/images/jq%20version.png)

### Check Delegators and Stake Command:
```
near view <your pool>.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId <accountId>.shardnet.near
```
![check delegator](../challenges/images/near%20view.png)
### Check Reason Validator Kicked Command:
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("<POOL_ID>"))' | jq .reason
```
### Check Blocks Produced / Expected Command:
```
curl -r -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.current_validators[] | select(.account_id | contains ("POOL_ID"))'
```
![check block produce](../challenges/images/check%20block%20produce.png)

 # Next Challenge
 [Chanllenge005](challenge005.md)
