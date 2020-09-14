FROM ubuntu:xenial

RUN apt-get update \
  && apt-get install -y wget software-properties-common \
  && rm -rf /var/lib/apt/lists/* \
  && add-apt-repository -y ppa:ethereum/ethereum \
  && apt-get update \
  && apt-get install -y ethereum

WORKDIR "/root"

COPY ./genesis.json ./
RUN geth init genesis.json

ARG password
RUN echo $password > ~/.accountpassword
ARG privatekey
RUN echo $privatekey > ~/.privatekey

RUN geth account import --password ~/.accountpassword  ~/.privatekey

#CMD exec geth --bootnodes enode://$bootnodeId@$bootnodeIp:30301 --networkid $networkId --verbosity=$verbosity --nousb --ws --wsport 8546 --wsaddr "0.0.0.0" --wsorigins="*" --wsapi=web3,net,admin --rpc --rpcport 8545 --rpcaddr "0.0.0.0" --rpcapi "eth,web3,net,admin,debug" --rpccorsdomain "*" --syncmode=$nodeType --etherbase $address --unlock $address --password ~/.accountpassword --allow-insecure-unlock
CMD exec geth --bootnodes enode://$bootnodeId@$bootnodeIp:30301 --networkid $networkId --verbosity=$verbosity --nousb --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,web3,net,admin,debug,miner,personal" --http.corsdomain "*" --ws --ws.addr "0.0.0.0" --ws.port 8546 --ws.api "eth,web3,net,admin,debug,miner,personal" --ws.origins "*" --syncmode=$nodeType --etherbase $address --unlock $address --password ~/.accountpassword --allow-insecure-unlock

EXPOSE 8545
EXPOSE 8546
EXPOSE 30303
