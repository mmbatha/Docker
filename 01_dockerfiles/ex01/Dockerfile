FROM debian

ENV TS3DIR=/opt/teamspeak

RUN apt-get update && apt-get upgrade -y && apt-get install bzip2 wget apt-utils ca-certificates -y --no-install-recommends && rm -rf /var/lib/apt/lists/* && \
wget https://files.teamspeak-services.com/releases/server/3.9.1/teamspeak3-server_linux_amd64-3.9.1.tar.bz2 -O /tmp/teamspeak.tar.bz2 && \
tar jxf /tmp/teamspeak.tar.bz2 -C /opt && \
mv /opt/teamspeak3-server_* ${TS3DIR} && \
rm /tmp/teamspeak.tar.bz2 && \
rm -rf /var/lib/apt/lists/*

RUN groupadd -g 503 teamspeakadmin && \
useradd -u 503 -g 503 -d ${TS3DIR} teamspeakadmin && \
mkdir /data && \
chown -R teamspeakadmin:teamspeakadmin ${TS3DIR} /data

ENV TS3SERVER_LICENSE=accept

USER teamspeakadmin
# Voice port
EXPOSE 9987/udp
# FTP port
EXPOSE 30033
# ServerQuery
EXPOSE 10011

WORKDIR $TS3DIR
ENTRYPOINT ["sh", "ts3server_minimal_runscript.sh"]

### Build server
# docker build -t ex01 .
### Run
# docker run -dit --init --rm --name ts3 -p 9987:9987/udp -p 10011:10011 -p 30033:30033 ex01
### Launch Teamspeak Client and Connect to 192.168.99.100:9877
