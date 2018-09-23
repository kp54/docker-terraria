FROM debian:jessie-slim
WORKDIR /terraria
RUN apt-get update && apt-get install -y wget unzip && \
    wget -O tmp.zip http://terraria.org/system/dedicated_servers/archives/000/000/032/original/terraria-server-1353.zip && \
    unzip tmp.zip && \
    cp -r 1353/Linux/* ./ && \
    chmod +x TerrariaServer.bin.x86_64 && \
    rm -r tmp.zip 1353 && \
    wget -O tmp.zip https://github.com/kp54/executor/files/2408464/executor-v1.0.1.zip &&\
    unzip tmp.zip && \
    rm tmp.zip && \
    apt-get purge -y wget unzip && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/*
COPY serverconfig.txt .
ENTRYPOINT [ "./executor", "./TerrariaServer.bin.x86_64", "exit", "-config", "serverconfig.txt" ]
