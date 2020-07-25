FROM ubuntu:bionic

RUN apt-get update \
  && apt-get install -y wget software-properties-common \
  && rm -rf /var/lib/apt/lists/* \
  && add-apt-repository -y ppa:ethereum/ethereum \
  && apt-get update \
  && apt-get install -y ethereum

WORKDIR "/root"

COPY ./genesis.json ./genesis.json
RUN geth init genesis.json

ARG password
RUN echo $password > ~/.accountpassword
ARG privatekey
RUN echo $privatekey > ~/.privatekey

RUN geth account import --password ~/.accountpassword  ~/.privatekey

CMD exec geth --bootnodes "enode://$bootnodeId@$bootnodeIp:30301" --nodekeyhex $nodekeyhex --networkid "$networkId" --nousb --verbosity=$verbosity  --syncmode=full --mine --shh --rpc --rpcaddr "0.0.0.0" --rpcapi "eth,web3,net,admin,debug,shh" --gasprice "0" --etherbase $address --unlock $address --password ~/.accountpassword --allow-insecure-unlock

#unavailable=[db] available="[admin debug web3 eth txpool personal clique miner net shh]"
#WARN [07-25|18:43:16.875] The flag --rpc is deprecated and will be removed in the future, please use --http
#WARN [07-25|18:43:16.875] The flag --rpcaddr is deprecated and will be removed in the future, please use --http.addr
#WARN [07-25|18:43:16.875] The flag --rpcapi is deprecated and will be removed in the future, please use --http.api
#INFO [07-25|18:43:16.875] Smartcard socket not found, disabling    err="stat /run/pcscd/pcscd.comm: no such file or directory"
#WARN [07-25|18:43:16.876] The flag --etherbase is deprecated and will be removed in the future, please use --miner.etherbase
#WARN [07-25|18:43:16.876] The flag --gasprice is deprecated and will be removed in the future, please use --miner.gasprice

EXPOSE 8545
EXPOSE 30303
