# 1、DW

## 1.1、当前的gas价格

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_gasPrice","params":[],"id":73}'`

##### 返回示例

```
 {`` "id":73,`` "jsonrpc": "2.0",`` "result": "0x09184e72a000" // 10000000000000``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**                 |
| ---------- | -------- | ------------------------ |
| result     | string   | 当前的gas价格，单位：wei |

## 1.2、返回指定地址账户的余额

##### 简要描述

- 返回指定地址账户的余额

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1",     "latest"],"id":1}'`

##### 参数

| **参数名** | **必选** | **类型** | **说明**                                                 |
| ---------- | -------- | -------- | -------------------------------------------------------- |
| DATA       | 是       | string   | 20字节，要检查余额的地址                                 |
| QUANTITY   | 是       | string   | 整数块编号，或者字符串"latest",  "earliest" 或 "pending" |

##### 返回示例

```
 {`` "id":1,`` "jsonrpc": "2.0",`` "result": "0x0234c8a3397aab58" // 158972490234375000``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**            |
| ---------- | -------- | ------------------- |
| result     | string   | 当前余额，单位：wei |

## 1.3、返回指定地址发生的交易数量

##### 简要描述

- 返回指定地址发生的交易数量

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x407d73d8a49eeb85d32cf465507dd71d507100c1","latest"],"id":1}'`

##### 参数

| **参数名** | **必选** | **类型** | **说明**                                                 |
| ---------- | -------- | -------- | -------------------------------------------------------- |
| DATA       | 是       | string   | 20字节，要检查余额的地址                                 |
| QUANTITY   | 是       | string   | 整数块编号，或者字符串"latest",  "earliest" 或 "pending" |

##### 返回示例

```
{`` "id":1,`` "jsonrpc": "2.0",`` "result": "0x1" // 1``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**                       |
| ---------- | -------- | ------------------------------ |
| result     | string   | 从指定地址发出的交易数量，整数 |

## 1.4、创建一个新的消息调用交易

##### 简要描述

- 创建一个新的消息调用交易，如果数据字段中包含代码，则创建一个合约

##### 参数

Object - 交易对象，结果如下：

from: DATA, 20字节 - 发送交易的源地址 to: DATA, 20字节 - 交易的目标地址，当创建新合约时可选 gas: QUANTITY - 交易执行可用gas量，可选整数，默认值90000，未用gas将返还。 gasPrice: QUANTITY - gas价格，可选，默认值：待定(To-Be-Determined) value: QUANTITY - 交易发送的金额，可选整数 data: DATA - 合约的编译带啊或被调用方法的签名及编码参数 nonce: QUANTITY - nonce，可选。可以使用同一个nonce来实现挂起的交易的重写

- `params:     [{ "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",     "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",     "gas": "0x76c0", // 30400 "gasPrice":     "0x9184e72a000", // 10000000000000 "value":     "0x9184e72a", // 2441406250 "data":     "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"     }]`

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_sendTransaction","params":[{see     above}],"id":1}'`

##### 返回示例

```
 {`` "id":1,`` "jsonrpc": "2.0",`` "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**                                         |
| ---------- | -------- | ------------------------------------------------ |
| result     | string   | 32字节 - 交易哈希，如果交易还未生效则返回0值哈希 |

## 1.5、为签名交易创建一个新的消息调用交易或合约

##### 简要描述

- 为签名交易创建一个新的消息调用交易或合约

##### 参数

DATA - 签名的交易数据

- `params:     ["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"]`

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":[{see     above}],"id":1}' `

##### 返回示例

```
 {`` "id":1,`` "jsonrpc": "2.0",`` "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**                                        |
| ---------- | -------- | ----------------------------------------------- |
| result     | string   | 32字节，交易哈希，如果交易未生效则返回全0哈希。 |

## 1.6、立刻执行一个新的消息调用，无需在区块链上创建交易。

##### 简要描述

- 立刻执行一个新的消息调用，无需在区块链上创建交易。

##### 参数

Object - 交易调用对象

from: DATA, 20 Bytes - 发送交易的原地址，可选 to: DATA, 20 Bytes - 交易目标地址 gas: QUANTITY - 交易可用gas量，可选。eth_call不消耗gas，但是某些执行环节需要这个参数 gasPrice: QUANTITY - gas价格，可选 value: QUANTITY - 交易发送的以太数量，可选 data: DATA - 方法签名和编码参数的哈希，可选 QUANTITY|TAG - 整数块编号，或字符串"latest"、"earliest"或"pending"

##### 请求

- `curl     -X POST --data '{"jsonrpc":"2.0","method":"eth_call","params":[{see     above}],"id":1}' `

##### 返回示例

```
 {`` "id":1,`` "jsonrpc": "2.0",`` "result": "0x"``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**           |
| ---------- | -------- | ------------------ |
| result     | string   | 所执行合约的返回值 |

## 1.7、执行并估算一个交易需要的gas用量

##### 简要描述

- 执行并估算一个交易需要的gas用量。该次交易不会写入区块链。注意，由于多种原因，例如EVM的机制     及节点旳性能，估算的数值可能比实际用量大的多。

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_estimateGas","params":[{see     above}],"id":1}'`

##### 参数

参考eth_call调用的参数，所有的属性都是可选的。如果没有指定gas用量上限，geth将使用挂起块的gas上限。 在这种情况下，返回的gas估算量可能不足以执行实际的交易。

##### 返回示例

```
 {`` "id":1,`` "jsonrpc": "2.0",`` "result": "0x5208" // 21000``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**      |
| ---------- | -------- | ------------- |
| result     | string   | gas用量估算值 |

## 1.8、返回具有指定哈希的块

##### 简要描述

- 返回具有指定哈希的块

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",     true],"id":1}'`

##### 参数

参数 DATA, 32字节 - 块哈希 Boolean - 为true时返回完整的交易对象，否则仅返回交易哈希

- `params:     [ '0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331',     true ]`

##### 返回示例

```
 {``"id":1,``"jsonrpc":"2.0",``"result": {``  "number": "0x1b4", // 436``  "hash": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",``  "parentHash": "0x9646252be9520f6e71339a8df9c55e4d7619deeb018d2a3f2d21fc165dde5eb5",``  "nonce": "0xe04d296d2460cfb8472af2c5fd05b5a214109c25688d3704aed5484f9a7792f2",``  "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",``  "logsBloom": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",``  "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",``  "stateRoot": "0xd5855eb08b3387c0af375e9cdb6acfc05eb8f519e419b874b6ff2ffda7ed1dff",``  "miner": "0x4e65fda2159562a496f9f3522f89122a3088497a",``  "difficulty": "0x027f07", // 163591``  "totalDifficulty": "0x027f07", // 163591``  "extraData": "0x0000000000000000000000000000000000000000000000000000000000000000",``  "size": "0x027f07", // 163591``  "gasLimit": "0x9f759", // 653145``  "gasUsed": "0x9f759", // 653145``  "timestamp": "0x54e34e8e" // 1424182926``  "transactions": [{...},{ ... }] ``  "uncles": ["0x1606e5...", "0xd5145a9..."]`` }``}
```

##### 返回参数说明

Object - 匹配的块对象，如果未找到块则返回null，结构如下： number: QUANTITY - 块编号，挂起块为null hash: DATA, 32 Bytes - 块哈希，挂起块为null parentHash: DATA, 32 Bytes - 父块的哈希 nonce: DATA, 8 Bytes - 生成的pow哈希，挂起块为null sha3Uncles: DATA, 32 Bytes - 块中叔伯数据的SHA3哈希 logsBloom: DATA, 256 Bytes - 快日志的bloom过滤器，挂起块为null transactionsRoot: DATA, 32 Bytes - 块中的交易树根节点 stateRoot: DATA, 32 Bytes - 块最终状态树的根节点 receiptsRoot: DATA, 32 Bytes - 块交易收据树的根节点 miner: DATA, 20 Bytes - 挖矿奖励的接收账户 difficulty: QUANTITY - 块难度，整数 totalDifficulty: QUANTITY - 截止到本块的链上总难度 extraData: DATA - 块额外数据 size: QUANTITY - 本块字节数 gasLimit: QUANTITY - 本块允许的最大gas用量 gasUsed: QUANTITY - 本块中所有交易使用的总gas用量 timestamp: QUANTITY - 块时间戳 transactions: Array - 交易对象数组，或32字节长的交易哈希数组 uncles: Array - 叔伯哈希数组

## 1.9、返回指定编号的块

##### 简要描述

- 返回指定编号的块

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4",     true],"id":1}' `

##### 参数

QUANTITY|TAG - 整数块编号，或字符串"earliest"、"latest" 或"pending" Boolean - 为true时返回完整的交易对象，否则仅返回交易哈希

```
params: [``  '0x1b4', // 436``  true``]
```

##### 返回示例

参考eth_getBlockByHash

## 1.10、返回指定哈希对应的交易

##### 简要描述

- 返回指定哈希对应的交易。

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'     `

##### 请求方式

- POST 

##### 参数

DATA, 32 字节 - 交易哈希

```
params: [``  "0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"``]
```

##### 返回示例

```
 {``"id":1,``"jsonrpc":"2.0",``"result": {``  "hash":"0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b",``  "nonce":"0x",``  "blockHash": "0xbeab0aa2411b7ab17f30a99d3cb9c6ef2fc5426d6ad6fd9e2a26a6aed1d1055b",``  "blockNumber": "0x15df", // 5599``  "transactionIndex": "0x1", // 1``  "from":"0x407d73d8a49eeb85d32cf465507dd71d507100c1",``  "to":"0x85h43d8a49eeb85d32cf465507dd71d507100c1",``  "value":"0x7f110", // 520464``  "gas": "0x7f110", // 520464``  "gasPrice":"0x09184e72a000",``  "input":"0x603880600c6000396000f300603880600c6000396000f3603880600c6000396000f360",`` }``}
```

##### 返回参数说明

Object - 交易对象，如果没有找到匹配的交易则返回null。结构如下：

hash: DATA, 32字节 - 交易哈希 nonce: QUANTITY - 本次交易之前发送方已经生成的交易数量 blockHash: DATA, 32字节 - 交易所在块的哈希，对于挂起块，该值为null blockNumber: QUANTITY - 交易所在块的编号，对于挂起块，该值为null transactionIndex: QUANTITY - 交易在块中的索引位置，挂起块该值为null from: DATA, 20字节 - 交易发送方地址 to: DATA, 20字节 - 交易接收方地址，对于合约创建交易，该值为null value: QUANTITY - 发送的以太数量，单位：wei gasPrice: QUANTITY - 发送方提供的gas价格，单位：wei gas: QUANTITY - 发送方提供的gas可用量 input: DATA - 随交易发送的数据

## 1.11、返回指定交易的收据，使用哈希指定交易

##### 简要描述

- 返回指定交易的收据，使用哈希指定交易

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}'     `

##### 参数

DATA, 32字节 - 交易哈希

```
params: [``  '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238'``]
```

##### 返回示例

```
 {``"id":1,``"jsonrpc":"2.0",``"result": {``   transactionHash: '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238',``   transactionIndex: '0x1', // 1``   blockNumber: '0xb', // 11``   blockHash: '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',``   cumulativeGasUsed: '0x33bc', // 13244``   gasUsed: '0x4dc', // 1244``   contractAddress: '0xb60e8dd61c5d32be8058bb8eb970870f07233155', // or null, if none was created``   logs: [{``     // logs as returned by getFilterLogs, etc.``   }, ...],``   logsBloom: "0x00...0", // 256 byte bloom filter``   status: '0x1'`` }``}
```

##### 返回参数说明

Object - 交易收据对象，如果收据不存在则为null。交易对象的结构如下：

transactionHash: DATA, 32字节 - 交易哈希 transactionIndex: QUANTITY - 交易在块内的索引序号 blockHash: DATA, 32字节 - 交易所在块的哈希 blockNumber: QUANTITY - 交易所在块的编号 from: DATA, 20字节 - 交易发送方地址 to: DATA, 20字节 - 交易接收方地址，对于合约创建交易该值为null cumulativeGasUsed: QUANTITY - 交易所在块消耗的gas总量 gasUsed: QUANTITY - 该次交易消耗的gas用量 contractAddress: DATA, 20字节 - 对于合约创建交易，该值为新创建的合约地址，否则为null logs: Array - 本次交易生成的日志对象数组 logsBloom: DATA, 256字节 - bloom过滤器，轻客户端用来快速提取相关日志 返回的结果对象中还包括下面二者之一 :

root : DATA 32字节，后交易状态根(pre Byzantium) status: QUANTITY ，1 (成功) 或 0 (失败)

## 1.12、返回最新块的编号

##### 简要描述

- 返回最新块的编号

##### 请求

- `curl     -X POST --data     '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":83}'     `

##### 请求方式

- POST 

##### 返回示例

```
{``  "id":83,`` "jsonrpc": "2.0",`` "result": "0x4b7" // 1207``}
```

##### 返回参数说明

| **参数名** | **类型** | **说明**       |
| ---------- | -------- | -------------- |
| result     | string   | 节点当前块编号 |

 