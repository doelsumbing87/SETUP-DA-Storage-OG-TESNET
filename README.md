## 🟢 Storage Node

### Persyaratan:
- **Storage Node:** Stake 0.1 Token dan siapkan fee di wallet yang digunakan.
- **DA Client:** Tidak membutuhkan stake.
- **Claim:** Melalui Discord.
- **Stake:** Di website resmi http://0g.exploreme.pro/validators

### Spesifikasi Minimum:
- **RAM:** 32 GB
- **CPU:** 8 Core
- **Storage:** 1TB SSD
- **Kecepatan Internet:** 100 MBPS Down/Up

### Instalasi:
```bash
screen -R storagenode

sudo apt-get update
sudo apt-get install clang cmake build-essential

cd $HOME && \
ver="1.22.0" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile && \
source ~/.bash_profile && \
go version
```

### Instalasi Rust:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
. "$HOME/.cargo/env"
```

### Clone Repository:
```bash
git clone https://github.com/0glabs/0g-storage-node.git
cd 0g-storage-node
git checkout v0.8.4
git submodule update --init
```

### Instalasi Cargo dan Dependensi:
```bash
sudo apt install cargo
sudo apt update
sudo apt install -y pkg-config libssl-dev
```

### Build Storage Node:
```bash
cargo build --release
```

### Konfigurasi Storage Node:
```bash
wget -O $HOME/0g-storage-node/run/config-testnet-turbo.toml https://josephtran.co/config-testnet-turbo.toml
```

```bash
printf '\033[34mEnter your private key: \033[0m' && read -s PRIVATE_KEY
```
Masukkan Private Key Anda.

```bash
sed -i 's|^\s*#?\s*miner_key\s*=.*|miner_key = "'$PRIVATE_KEY'"|' $HOME/0g-storage-node/run/config-testnet-turbo.toml && echo -e "\033[32mPrivate key has been successfully added to the config file.\033[0m"
```

Verifikasi Konfigurasi:
```bash
grep -E "^(network_dir|network_enr_address|network_enr_tcp_port|network_enr_udp_port|network_libp2p_port|network_discovery_port|rpc_listen_address|rpc_enabled|db_dir|log_config_file|log_contract_address|mine_contract_address|reward_contract_address|log_sync_start_block_number|blockchain_rpc_endpoint|auto_sync_enabled|find_peer_timeout)" $HOME/0g-storage-node/run/config-testnet-turbo.toml
```

Selesai! 🎉
