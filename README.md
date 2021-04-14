# starcoin-vs-ethereum-rpc
Starcoin vs. Ethereum - JSON RPC comparison

## Postman JSON RPC test

We have provided Ethereum and Starcoin JSON RPC API collections in this repo. You could import them and test conveniently.

#### Testing Ethereum

1. Go to Postman Workspace page, then import `ethereum.postman_collection.json`
2. Go to Postman Environments page, then import `ethereum.postman_environment.json`
3. Go to [Infura.io](https://infura.io), choose an Ethereum network(for example, `kovan`) and get your `project_id`
4. Modify the network name and `project_id` in Postman ethereum Environments with your own
5. Choose an API, and click **Send** button

#### Testing Starcoin

1. Go to Postman Workspace page, then import `starcoin.postman_collection.json`
2. Go to Postman Environments page, then import `starcoin.postman_environment.json`
3. Run your local Starcoin network, or join online Starcoin network, like `barnard`, please refer to official Starcoin [documentation](https://developer.starcoin.org/en/setup/runnetwork/). The difference is that here we will open all Websocket and HTTP APIs for testing. For security, please do not tell your node URL to others.

Start barnard node
```
./starcoin -n barnard --push-server-url http://miner-metrics-pushgw.starcoin.org:9191/ --push-interval 60 --miner-thread 4 --websocket-apis all --http-apis all
```

Start local dev node
```
./starcoin -n dev --miner-thread 2 --websocket-apis all --http-apis all
```

4. Modify the URL in Postman starcoin environments with your own
5. Choose an API, and click **Send** button


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
| `eth_getBlockTransactionCountByHash` | `chain.get_block_txn_infos` -> `result.length` |

Note: `chain.get_block_txn_infos` returns an array of all transactions on a block.

## Get transaction by hash

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionByHash` | `chain.get_transaction` |

## Get transaction by block hash and index

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionByBlockHashAndIndex` | `chain.get_txn_info_by_block_and_index` |

## Get transaction receipt

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionReceipt` | `chain.get_transaction` |

Note: `chain.get_transaction` returns information of an executed transaction. To get information of a pending transaction, please use `txpool.pending_txn`.

## Get transaction count of an account

| Ethereum | Starcoin |
| --- | --- |
| `eth_getTransactionCount` | `state.get_account_state_set` -> `result[result.length - 1][1].U64` |

Note: `state.get_account_state_set` returns a big array containing all information of an account, the number of transactions equals the `sequence_number` of the account.

## Get code for contract or module 

| Ethereum | Starcoin |
| --- | --- |
| `eth_getCode` | `contract.get_code` |

Note: you could get a list of Starcoin modules and their module_id here: [https://github.com/starcoinorg/starcoin/tree/master/vm/stdlib/modules/doc](https://github.com/starcoinorg/starcoin/tree/master/vm/stdlib/modules/doc)

## Get chain ID

| Ethereum | Starcoin |
| --- | --- |
| `net_version` | `chain.id` -> `result.id` |

Note: `eth_chainId` in Ethereum also returns the chain ID, but in hex format. The `chain.id` method in Starcoin will also return the chain name of Starcoin, for example, `barnard`, `proxima`, etc.

## Send transaction

| Ethereum | Starcoin |
| --- | --- |
| `eth_call` | `txpool.submit_hex_transaction` |

Note: hex transaction should be constructed from signer and transaction parameters, check the details out in [starcoin.js](https://github.com/starcoinorg/starcoin.js/blob/e844b2c1f871f686e8357f8131950f5122fc7fb1/src/providers/jsonrpc-provider.ts#L425).

## Get gas price

| Ethereum | Starcoin |
| --- | --- |
| `eth_gasPrice` | `txpool.gas_price` |

## Get peer count

| Ethereum | Starcoin |
| --- | --- |
| `net_peerCount` | `network_manager.known_peers` -> `result.length` |

Notes: `node.peers` in Starcoin will also returns a big array containing all peers' information.

## Get syncing status

| Ethereum | Starcoin |
| --- | --- |
| `eth_syncing` | `sync.status` |

---

## New Starcoin APIs not implemented in Ethereum

- `chain.get_blocks_by_number`
- `chain.get_transaction_info`

## Ethereum APIs not implemented in Starcoin yet

- `eth_estimateGas`
- `eth_getBlockTransactionCountByNumber`
- `eth_getTransactionByBlockNumberAndIndex`
