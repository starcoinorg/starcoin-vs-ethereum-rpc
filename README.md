# starcoin-vs-ethereum-rpc
Starcoin vs. Ethereum - JSON RPC comparison


## Get accounts

| Ethereum | Starcoin |
| --- | --- |
| `eth_accounts` | `account.list` |

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

## Get block by hash

| Ethereum | Starcoin |
| --- | --- |
| `eth_getBlockByHash` | `chain.get_block_by_hash` |

## Get transaction count on a block

| Ethereum | Starcoin |
| --- | --- |
| `eth_getBlockTransactionCountByHash` | `chain.get_block_txn_infos` -> result.length |

Note: `chain.get_block_txn_infos` returns an array of all transactions on a block.

## Get transaction by hash

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionByHash` | `chain.get_transaction` |

## Get transaction by block hash and index

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionByBlockHashAndIndex` | `chain.get_txn_info_by_block_and_index` |

## Get transaction count of an account

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionCount` | `state.get_account_state_set` -> result[result.length - 1][1].U64 |

Note: `state.get_account_state_set` returns an big array of all information of an account, the number of transactions equals the `sequence_number` of the account.

## Get chain ID

| Ethereum | Starcoin |
| --- | --- |
| `net_version` | `chain.id` -> `result.id` |

Note: `eth_chainId` in Ethereum also returns the chain ID, but in hex. The `chain.id` method in Starcoin will also return the chain name of Starcoin, for example, `barnard`, `proxima`, etc.

## Send transaction

| Ethereum | Starcoin |
| --- | --- |
| `eth_call` | `txpool.submit_hex_transaction` |

Note: hex transaction should be constructed from signer and transaction parameters, check this in [starcoin.js](https://github.com/starcoinorg/starcoin.js/src/providers/jsonrpc-provider.ts).

## Get gas price

| Ethereum | Starcoin |
| --- | --- |
| `eth_gasPrice` | `txpool.gas_price` |

---

## New Starcoin APIs not implemented in Ethereum

- `chain.get_blocks_by_number`
- `chain.get_transaction_info`

## Ethereum APIs not implemented in Starcoin yet

- `eth_estimateGas`
- `eth_getBlockTransactionCountByNumber`
- `eth_getTransactionByBlockNumberAndIndex`
