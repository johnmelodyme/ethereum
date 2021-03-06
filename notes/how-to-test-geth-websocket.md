### How to test Geth's WebSocket Pub/Sub?

#### 1 - Install `wscat` CLI

`$ yarn global add wscat`

Learn more about `wscat` package [here](https://www.npmjs.com/package/wscat).

All options provided by the package:

```
$ wscat --help

  Usage: wscat [options] (--listen <port> | --connect <url>)


  Options:

    -V, --version                 output the version number
    -l, --listen <port>           listen on port
    -c, --connect <url>           connect to a websocket server
    -p, --protocol <version>      optional protocol version
    -o, --origin <origin>         optional origin
    -x, --execute <command>       execute command after connecting
    -w, --wait <seconds>          wait given seconds after executing command
    --host <host>                 optional host
    -s, --subprotocol <protocol>  optional subprotocol
    -n, --no-check                Do not check for unauthorized certificates (default: true)
    -H, --header <header:value>   Set an HTTP header. Repeat to set multiple. (--connect only) (default: )
    --auth <username:password>    Add basic HTTP authentication header. (--connect only)
    --ca <ca>                     Specify a Certificate Authority (--connect only)
    --cert <cert>                 Specify a Client SSL Certificate (--connect only)
    --key <key>                   Specify a Client SSL Certificate's key (--connect only)
    --passphrase [passphrase]     Specify a Client SSL Certificate Key's passphrase (--connect only). If you don't provide a value, it will be prompted for.
    --no-color                    Run without color (default: true)
    -h, --help                    output usage information
```

#### 2 - Start the WebSocket client

`$ wscat --connect ws://server-ip:ws-port --protocol 13`

For example:

`$ wscat --connect ws://192.168.0.170:8547 --protocol 13`

#### 3 - Use it

Learn more about Geth's Pub/Sub [here](https://github.com/ethereum/go-ethereum/wiki/RPC-PUB-SUB).

```
$ wscat --connect ws://192.168.0.170:8547 --protocol 13
connected (press CTRL+C to quit)
> {"id": 1, "method": "eth_subscribe", "params": ["newHeads", {}]}
< {"jsonrpc":"2.0","id":1,"result":"0xa48a8032dc75ac309512765baac04483"}

< {"jsonrpc":"2.0","method":"eth_subscription","params":{"subscription":"0xa48a8032dc75ac309512765baac04483","result":{"parentHash":"0x6e1a14349034ba58aa94c98d12ba1070b5b4d2d1a5b766f7356955b2d2c2655e","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","miner":"0xa07530748603380e03d59d33e51cae7e3d57984d","stateRoot":"0x114cb5ebd3dfa7c6e1dfa90af256b1063931dd0af634c6c8b0a5898108d70c10","transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","difficulty":"0xcace3","number":"0x19c9","gasLimit":"0x47e7c4","gasUsed":"0x0","timestamp":"0x5a29237c","extraData":"0xd583010703846765746885676f312e39856c696e7578","mixHash":"0x663a556e8be8d6baf966116dd10308cf98877cbc20040bbf94f2b46feded2012","nonce":"0x486c2ba1ac5ca08a","hash":"0x70287677a6dccbf9fef6f279d25a563a08f7b11640737d2540da2cf92c0ae84b"}}}

< {"jsonrpc":"2.0","method":"eth_subscription","params":{"subscription":"0xa48a8032dc75ac309512765baac04483","result":{"parentHash":"0x70287677a6dccbf9fef6f279d25a563a08f7b11640737d2540da2cf92c0ae84b","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","miner":"0xa07530748603380e03d59d33e51cae7e3d57984d","stateRoot":"0xaed0abc3b98d93c1e7611aa513383a9a0aaeb9a8ed5b264a5150126d6a39fe03","transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421","logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","difficulty":"0xca9b9","number":"0x19ca","gasLimit":"0x47e7c4","gasUsed":"0x0","timestamp":"0x5a29239c","extraData":"0xd583010703846765746885676f312e39856c696e7578","mixHash":"0x571ed30c8272c10214ad8a23fd9bc1a4f8b28eb303b82d2a2a047b177bc1b4da","nonce":"0x1a9a75db7859e460","hash":"0x06b171c03172a573579b04ffa14cd82f22c608bad354cc1be2f4b4f832a8d9d0"}}}

> {"id": 1, "method": "eth_unsubscribe", "params": ["0xa48a8032dc75ac309512765baac04483"]}
< {"jsonrpc":"2.0","id":1,"result":true}
```

Example of the responses (pretty):

```
{
   "jsonrpc":"2.0",
   "method":"eth_subscription",
   "params":{
      "subscription":"0x49dfd9596879e2ed6c37ff4376b44d2e",
      "result":{
         "parentHash":"0x10d1bd1bcb5aaee5d26e0df66855b5a314de373c774cb7f9b2461e561377d57a",
         "sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
         "miner":"0xa07530748603380e03d59d33e51cae7e3d57984d",
         "stateRoot":"0x975b47dbbabd3f6c789c5340c751333640d5878cbdcda9f4b50be8b7acfdd5ff",
         "transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
         "receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
         "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
         "difficulty":"0xaf541",
         "number":"0x15a9",
         "gasLimit":"0x47e7c4",
         "gasUsed":"0x0",
         "timestamp":"0x5a28f2b6",
         "extraData":"0xd583010703846765746885676f312e39856c696e7578",
         "mixHash":"0x5d7f80f0677af95b2cb938476c69246c45d2fb45dd4cb01553e35fd85eb0f2f7",
         "nonce":"0x7279154b3baba0f8",
         "hash":"0x15986dfdad35d7ded750af22751683038d4d260a1c814950130e54ed8d48bf26"
      }
   }
},
{
   "jsonrpc":"2.0",
   "method":"eth_subscription",
   "params":{
      "subscription":"0x49dfd9596879e2ed6c37ff4376b44d2e",
      "result":{
         "parentHash":"0x15986dfdad35d7ded750af22751683038d4d260a1c814950130e54ed8d48bf26",
         "sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
         "miner":"0xa07530748603380e03d59d33e51cae7e3d57984d",
         "stateRoot":"0xc17b6c836de359d84a470ef6392ffd016886f62f71436ec31044e22bffe729bb",
         "transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
         "receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
         "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
         "difficulty":"0xaf69f",
         "number":"0x15aa",
         "gasLimit":"0x47e7c4",
         "gasUsed":"0x0",
         "timestamp":"0x5a28f2b9",
         "extraData":"0xd583010703846765746885676f312e39856c696e7578",
         "mixHash":"0x4137d03a73ce462d90152f7e33d5180282fd2818f48238c920822991921d9094",
         "nonce":"0x2b479a3007ccd516",
         "hash":"0x243b6a2367f9e4f40a8f48efd98af488f525f32e6098f6940d7f2dc3151d1558"
      }
   }
}
```
