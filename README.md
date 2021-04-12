# starcoin-vs-ethereum-rpc
Starcoin vs Ethereum JSON RPC comparison


## Get accounts

| Ethereum | Starcoin |
| --- | --- |
| `eth_accounts` | `account.list`

## Get account balance

| Ethereum | Starcoin |
| --- | --- |
| `eth_getBalance` | `contract.get_resource` -> `result.value[0][1].Struct.value[0][1].U128` |

## Get latest block number

| Ethereum | Starcoin |
| --- | --- |
| `eth_blockNumber` | `chain.info` -> `result.header.number` |

## Get block by number

| Ethereum | Starcoin |
| --- | --- |
| `eth_getBlockByNumber` | `chain.get_block_by_number` |

## Get chain ID

| Ethereum | Starcoin |
| --- | --- |
| `net_version` | `chain.id` -> `result.id` |

Note: `eth_chainId` in Ethereum also return the chain ID, but in hex. The `chain.id` method in Starcoin will also return the chain name of starcoin, for example, `barnard`, `proxima`, etc.

## Send transaction

| Ethereum | Starcoin |
| --- | --- |
| `eth_call` | `txpool.submit_hex_transaction` 

Note: hex transaction should be constructed from signer and transaction parameters, check this in [starcoin.js](https://github.com/starcoinorg/starcoin.js).
