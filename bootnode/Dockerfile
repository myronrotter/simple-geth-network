FROM ubuntu:xenial

RUN apt-get update \
  && apt-get install -y wget software-properties-common \
  && rm -rf /var/lib/apt/lists/* \
  && add-apt-repository -y ppa:ethereum/ethereum \
  && apt-get update \
  && apt-get install -y ethereum

WORKDIR "/root"

CMD exec bootnode -nodekeyhex $nodekeyhex -addr $bootnodeIp:30301 -verbosity=$verbosity

EXPOSE 30301/udp
EXPOSE 30303/udp
