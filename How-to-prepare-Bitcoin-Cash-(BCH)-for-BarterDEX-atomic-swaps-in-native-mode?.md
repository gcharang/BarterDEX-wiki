You need Bitcoin Cash (BCH) blockchain synced and the wallet daemon running.

Compile and run BitcoinABC wallet from source:

```shell
git clone https://github.com/Bitcoin-ABC/bitcoin-abc
cd bitcoin-abc
./autogen.sh
./configure --with-incompatible-bdb --with-gui=no --disable-tests --disable-bench --without-miniupnpc
make -j4
sudo mv src/bitcoind /usr/local/bin/bchd
sudo mv src/bitcoin-cli /usr/local/bin/bch-cli
sudo mv src/bitcoin-tx /usr/local/bin/bch-tx
mkdir ~/.bch
echo "server=1" >> ~/.bch/bch.conf
echo "listen=0" >> ~/.bch/bch.conf
echo "listenonion=0" >> ~/.bch/bch.conf
echo "rpcport=33333" >> ~/.bch/bch.conf
echo "rpcuser=barterbch" >> ~/.bch/bch.conf
echo "rpcpassword=`head -c 32 /dev/urandom | base64`" >> ~/.bch/bch.conf
chmod 0600 ~/.bch/bch.conf
bchd -daemon -datadir=~/.bch -conf=bch.conf
```

If you already have this installed, just run `bchd -datadir=/home/<user>/.bch -conf=bch.conf -prune=4096 -daemon`

If you already have Bitcoin ABC istalled on MacOS, you can restart using this command:
```shell
./BitcoinABC-Qt -conf=$HOME/Library/Application\ Support/Bch/bch.conf  -datadir=$HOME/Library/Application\ Support/Bch/
```

Basically, just run the daemon with `.bch/bch.conf` for native and then start BarterDEX and test. That means to run Bitcoin Cash with BarterDEX the BCH users `must` change their Bitcoin Cash data directory, setup `bitcoin.conf` as `bch.conf` file.

`bch.conf` file contents:
```JSON
rpcuser=examplerpcuser
rpcpassword=examplerpcpassword
prune=4096
server=1
rpcbind=127.0.0.1
bind=127.0.0.1
rpcport=33333
```

BaterDEX GUI will automatically show you BitcoinCash (BCH)

Use RPC commands like this `bch-cli -datadir=/home/<user>/.bch -conf=bch.conf getinfo` to query data.

Optional: This entry goes to `coins.json` file (add this if this is not there).
`{\"coin\":\"BCH\",\"name\":\"bch\",\"active\":1,\"rpcport\":33333,\"pubtype\":0,\"p2shtype\":5,\"wiftype\":128,\"txfee\":1000}`
