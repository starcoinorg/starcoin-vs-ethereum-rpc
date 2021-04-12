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
| `eth_chainId` | `chain.id` -> `result.id` |

## Get network version

| Ethereum | Starcoin |
| --- | --- |
| `net_version` | `chain.id` -> `result.name` |
