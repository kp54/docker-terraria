ARG TERRARIA_VERSION="1353"

FROM golang:stretch as builder

WORKDIR /tmp

RUN apt-get update && apt-get install -y wget unzip git
RUN wget http://terraria.org/system/dedicated_servers/archives/000/000/032/original/terraria-server-${TERRARIA_VERSION}.zip
RUN unzip terraria-server-${TERRARIA_VERSION}.zip
RUN chmod +x ${TERRARIA_VERSION}/Linux/TerrariaServer.bin.x86_64
RUN git clone https://github.com/kp54/executor/
RUN cd executor && go build

RUN mkdir dist
RUN cp -r ${TERRARIA_VERSION}/Linux/* dist/
RUN cp executor/executor dist/


FROM debian:jessie-slim

WORKDIR /terraria

COPY --from=builder /tmp/dist/* ./

ENTRYPOINT [ "./executor", "./TerrariaServer.bin.x86_64", "exit", "-config", "config/serverconfig.txt" ]
