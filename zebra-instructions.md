# How to mine with Zebra on testnet

`s-nomp` has not been updated for NU5, so these instructions will get you an error like:

> 2023-02-01T06:26:32.873143Z  INFO zebra_rpc::methods::get_block_template_rpcs: submit block failed error=Ok(Block { source: Transaction(CoinbaseExpiryBlockHeight { expiry_height: None, block_height: Height(2212538), transaction_hash: transaction::Hash("de0eaaec7ed09500da395f6def5d14b173b57f4f331874fd6703753fbb933346") }) }) block_height="2212538"

## Install and run a mining pool

Install dependencies:
1. Install `redis` and run it on the default port: https://redis.io/docs/getting-started/
2. Install and activate `nodenv`: https://github.com/nodenv/nodenv#installation
3. Install `boost` and `libsodium`

Install `s-nomp`:
1. `git clone https://github.com/teor2345/s-nomp`
2. `cd s-nomp`
3. Use the Zebra configs: `git checkout zebra-mining`
4. Use node 8.17.0:
```sh
nodenv install 8.17.0
nodenv local 8.17.0
```
5. Update dependencies and install:
```sh
# TODO: is this needed?
export CXXFLAGS="-std=gnu++17"
npm update
npm install
```

Run `s-nomp`:
1. Edit `pool_configs/zclassic.json` so it has your Zebra port
2. Run `s-nomp` using `npm start`

Note: the website will log an RPC error even when disabled, this seems like a `s-nomp` bug

## Install a CPU or GPU miner

Install dependencies:
1. Install a statically compiled `boost` and `icu`
2. Optional: install static CUDA GPU mining libraries: https://github.com/ZclassicDev/GCEQminer#general-instructions

Install miner:
1. `git clone https://github.com/teor2345/nheqminer`
2. `cd nheqminer`
3. Use the Zebra fixes: `git checkout zebra-mining`
4. Follow the build instructions: https://github.com/nicehash/nheqminer#general-instructions
```sh
mkdir build && cd build
# if you have CUDA installed, you can leave USE_CUDA_DJEZO on 
cmake -DUSE_CUDA_DJEZO=OFF ..
make -j $(nproc)
```

Run miner:
1. Follow the run instructions at: https://github.com/ZclassicDev/GCEQminer#run-instructions
```sh
# or use your testnet address here
./nheqminer -l 127.0.0.1:1234 -u tmRGc4CD1UyUdbSJmTUzcB6oDqk4qUaHnnh.worker1 -t 1
```

## TODO

Do we want to fix the missing or incorrect values in the `s-nomp` stats logs?
```
Network Connected:      Mainnet - missing or incorrect RPC, or config issue?
Detected Reward Type:   POW
Current Block Height:   2212372
Current Block Diff:     0.050878195
Current Connect Peers:  undefined - missing getpeers RPC field?
Network Difficulty:     NaN - missing getdifficulty? RPC
Network Hash Rate:      0.00 KH - missing RPC?
Stratum Port(s):        1234
Pool Fee Percent:       0.2%
Block polling every:    500 ms
```
