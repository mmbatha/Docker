FROM		debian

LABEL		Author="Monde MBATHA <mmbatha@student.42.fr>" \
			Description="Debian-based container that runs a teamspeak server to be used by the Teamspeak 3 Client" \
			License="MIT License 2.0" \
			Usage="docker run -dit --init --rm --name ts3 -p [TS3_VOICE_PORT]:9987/udp -p [TS3_SERVER_QUERY_PORT]:10011 -p [TS3_VOICE_PORT]:30033 ex01"

ENV			TS3DIR=/opt/teamspeak

RUN			apt-get update && apt-get upgrade -y && apt-get install bzip2 wget apt-utils ca-certificates locales -y  && locale-gen en_ZA.UTF-8 && rm -rf /var/lib/apt/lists/* && wget https://files.teamspeak-services.com/releases/server/3.9.1/teamspeak3-server_linux_amd64-3.9.1.tar.bz2 -O /tmp/teamspeak.tar.bz2 && tar jxf /tmp/teamspeak.tar.bz2 -C /opt && mv /opt/teamspeak3-server_* ${TS3DIR} && rm /tmp/teamspeak.tar.bz2 && rm -rf /var/lib/apt/lists/* && groupadd -g 503 teamspeakadmin && useradd -u 503 -g 503 -d ${TS3DIR} teamspeakadmin && mkdir /data && chown -R teamspeakadmin:teamspeakadmin ${TS3DIR} /data

ENV			TS3SERVER_LICENSE=accept

USER		teamspeakadmin
# Voice port # FTP port # ServerQuery
EXPOSE		9987/udp 30033 10011

WORKDIR		$TS3DIR

ENTRYPOINT	["sh", "ts3server_minimal_runscript.sh"]

### Build server
# docker build -t ex01 .
### Run
# docker run -dit --init --rm --name ts3server -p 9987:9987/udp -p 10011:10011 -p 30033:30033 ex01
### Launch Teamspeak 3 Client and Connect to $(docker ip Char):9987
