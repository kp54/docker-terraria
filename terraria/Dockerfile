FROM golang:stretch as builder

WORKDIR /tmp

RUN apt-get update && apt-get install -y wget unzip git
RUN wget http://terraria.org/system/dedicated_servers/archives/000/000/032/original/terraria-server-1353.zip 
RUN unzip terraria-server-1353.zip
RUN chmod +x 1353/Linux/TerrariaServer.bin.x86_64
RUN git clone https://github.com/kp54/executor/
RUN cd executor && go build

RUN mkdir dist
RUN cp -r 1353/Linux/* dist/
RUN cp executor/executor dist/


FROM debian:jessie-slim

WORKDIR /terraria

COPY --from=builder /tmp/dist/* ./
COPY serverconfig.txt .

ENTRYPOINT [ "./executor", "./TerrariaServer.bin.x86_64", "exit", "-config", "serverconfig.txt" ]
