# Challenge 003

## Mounting a staking pool

```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```
* Pool ID: Staking pool name, the factory automatically adds its name to this parameter, creating {pool_id}.{staking_pool_factory} Examples:
* If pool id is stakewars will create : stakewars.factory.shardnet.near
* Owner ID: The SHARDNET account (i.e. stakewares.shardnet.near) that will manage the staking pool.
* Public Key: The public key in your validator_key.json file.
* 5: The fee the pool will charge (e.g. in this case 5 over 100 is 5% of fees).
* Account Id: The SHARDNET account deploying and signing the mount tx. Usually the same as the Owner ID.

**example:**
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "vicmeo", "owner_id": "vicmeo.shardnet.near", "stake_public_key": "ed25519:2jprrcWXXeBz2KgDr4i4owoPn7aHHSXLUzhZWENhE24k", "reward_fee_fraction": {"numerator": 1, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="vicmeo.shardnet.near" --amount=1111 --gas=300000000000000
```
![mount staking pool](../challenges/images/mount%20staking.png)

## Transactions Guide:

### Unstake Near
```
near call <staking_pool_id> unstake '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```
### Deposit and Stake NEAR
```
near call <staking_pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000
```
### Unstake NEAR
Amount in yoctoNEAR:
```
near call <staking_pool_id> unstake '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```
### To unstake all you can run this one:
```
near call <staking_pool_id> unstake_all --accountId <accountId> --gas=300000000000000
```

### Withdraw
Unstaking takes 2–3 epochs to complete, after that period you can withdraw in YoctoNEAR from pool:
```
near call <staking_pool_id> withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```
Command to withdraw all:
```
near call <staking_pool_id> withdraw_all --accountId <accountId> --gas=300000000000000
```
### Ping
A ping issues a new proposal and updates the staking balances for your delegators. A ping should be issued each epoch to keep reported rewards current.

```
near call <staking_pool_id> ping '{}' --accountId <accountId> --gas=300000000000000
```

### Balances Total Balance

```
near view <staking_pool_id> get_account_total_balance '{"account_id": "<accountId>"}'
```

### Staked Balance
```
near view <staking_pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
```
### Unstaked Balance
```
near view <staking_pool_id> get_account_unstaked_balance '{"account_id": "<accountId>"}'
```
### Available for Withdrawal
You can only withdraw funds from a contract if they are unlocked.
```
near view <staking_pool_id> is_account_unstaked_balance_available '{"account_id": "<accountId>"}'
```
### Pause / Resume Staking

* Pause
```
near call <staking_pool_id> pause_staking '{}' --accountId <accountId>
```
* Resume
```
near call <staking_pool_id> resume_staking '{}' --accountId <accountId>
```
 # Next Challenge
 [Chanllenge004](challenge004.md)