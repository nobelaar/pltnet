# 🪙 PLT Blockchain

**PLT** is a sovereign blockchain built using the **Cosmos SDK** and **CometBFT (Tendermint)** consensus engine.
Originally scaffolded with [Ignite CLI](https://ignite.com/cli), PLT now runs as an independent chain and can be compiled, initialized, and started manually.

---

## ⚙️ Requirements

* Go **1.22+**
* GNU Make, git, curl, jq
* Linux / macOS environment

---

## 🧩 Installation

Clone and build the binary:

```bash
git clone https://github.com/nobelaar/pltnet
cd pltnet
go mod tidy
go build -o ~/go/bin/pltd ./cmd/pltd
```

Verify installation:

```bash
pltd version
```

---

## 🌱 Initialize the Node

Create the local config and genesis file:

```bash
pltd init bootstrap --chain-id plt-test0
```

This creates the config directory at:

```
~/.plt/config/
```

---

## 🔑 Create a Local Key

Generate a new keypair to act as the bootstrap account:

```bash
pltd keys add bootstrap
```

Save the mnemonic phrase safely — it’s the only way to recover your funds.

---

## 💰 Add Genesis Account

Allocate initial tokens to your account:

```bash
pltd genesis add-genesis-account bootstrap 1000000000uplt
```

---

## 🏗️ Generate the Validator Transaction

Create a validator self-delegation transaction:

```bash
pltd genesis gentx bootstrap 1000000uplt --chain-id plt-test0
```

---

## 📦 Collect Genesis Transactions

Combine all gentxs (in this case only your own):

```bash
pltd genesis collect-gentxs
```

---

## ✅ Validate the Genesis

Before starting the chain, verify that the genesis file is valid:

```bash
pltd genesis validate-genesis
```

---

## 🚀 Start the Node

Edit `~/.plt/config/app.toml` and set:

```toml
minimum-gas-prices = "0.001uplt"
```

Then start your node:

```bash
pltd start
```

If you see logs similar to this, your node is live:

```
INF Starting ABCI server module=server
INF Starting P2P Node module=p2p
INF Starting RPC HTTP server on tcp://127.0.0.1:26657
```

---

## 🌐 Accessing the Node

* **Status**:

  ```bash
  curl http://127.0.0.1:26657/status
  ```

* **gRPC**: `localhost:9090`

* **REST API**: `localhost:1317`

---

## 🔗 Public Node (Optional)

To expose your node publicly:

1. Edit `~/.plt/config/config.toml`

   ```toml
   laddr = "tcp://0.0.0.0:26656"
   external_address = "tcp://<YOUR_PUBLIC_IP>:26656"
   ```

2. Open ports:

   ```bash
   sudo ufw allow 26656 26657 1317 9090
   ```

3. Get your peer ID:

   ```bash
   pltd tendermint show-node-id
   ```

   Share as:

   ```
   <node_id>@<ip>:26656
   ```

---

## 📚 References

* [Cosmos SDK Documentation](https://docs.cosmos.network)
* [CometBFT (Tendermint)](https://docs.cometbft.com)
* [Ignite CLI](https://docs.ignite.com)
