FROM        --platform=$TARGETOS/$TARGETARCH debian:buster-slim

LABEL       org.opencontainers.image.source="https://github.com/SimixHD/java"
LABEL       org.opencontainers.image.licenses=MIT

RUN 	    apt update && apt upgrade -y \
    		&& apt install -y --no-install-recommends \
        	gcc g++ libgcc1 libc++-dev gdb libc6 git wget curl tar zip unzip binutils xz-utils liblzo2-2 cabextract iproute2 net-tools telnet libatomic1 libsdl1.2debian libsdl2-2.0-0 \
        	libfontconfig libicu-dev libunwind8 libssl-dev sqlite3 libsqlite3-dev libmariadb-dev libmariadb-dev-compat locales ffmpeg gnupg2 apt-transport-https software-properties-common ca-certificates tzdata \
        	lua5.3 libz-dev rapidjson-dev \
            && install -m 0755 -d /etc/apt/keyrings \
            && curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc \
            && chmod a+r /etc/apt/keyrings/docker.asc \
            && echo \
              "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
              buster stable" | \
              tee /etc/apt/sources.list.d/docker.list > /dev/null \
            && apt-get update \
            && apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin \
    		&& dpkg-reconfigure --frontend noninteractive locales \
    		&& useradd -m -d /home/container -s /bin/bash container \
    		&& apt clean && rm -rf /var/lib/apt/lists/*

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
