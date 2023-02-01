# How to run s-nomp with Zebra

Install dependencies:
1. Install `redis` and run it on the default port: https://redis.io/docs/getting-started/
2. Install and activate `nodenv`: https://github.com/nodenv/nodenv#installation

Install `s-nomp`:
1. Clone https://github.com/teor2345/s-nomp/tree/zebra-mining
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

TODO:
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
