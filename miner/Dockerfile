FROM ubuntu:xenial

RUN apt-get update \
  && apt-get install -y wget software-properties-common \
  && rm -rf /var/lib/apt/lists/* \
  && add-apt-repository -y ppa:ethereum/ethereum \
  && apt-get update \
  && apt-get install -y ethereum

WORKDIR "/root"

#COPY ./static-nodes.json ./.ethereum/static-nodes.json
COPY ./genesis.json ./
RUN geth init genesis.json

ARG password
RUN echo $password > ~/.accountpassword
ARG privatekey
RUN echo $privatekey > ~/.privatekey

RUN geth account import --password ~/.accountpassword  ~/.privatekey

CMD exec geth --bootnodes enode://$bootnodeId@$bootnodeIp:30301 --nodekeyhex $nodekeyhex --networkid $networkId --verbosity=$verbosity --syncmode=full --nousb --mine --miner.gasprice 0 --miner.etherbase $address --unlock $address --password ~/.accountpassword --allow-insecure-unlock
#CMD exec geth --nodekeyhex $nodekeyhex --networkid $networkId --verbosity=$verbosity --syncmode=full --nousb --mine --miner.gasprice 0 --miner.etherbase $address --unlock $address --password ~/.accountpassword --allow-insecure-unlock

EXPOSE 30303
