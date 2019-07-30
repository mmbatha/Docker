FROM ubuntu:16.04

RUN apt-get update && apt-get upgrade -y && apt-get install -y ca-certificates openssh-server wget postfix

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && chmod 777 script.deb.sh && ./script.deb.sh && apt-get install -y gitlab-ce=11.11.2-ce.0

RUN apt-get update && apt-get install -y tzdata && apt-get clean && rm -rf /var/lib/apt/lists/ /tmp/ /var/tmp/*

EXPOSE 443 80 22

RUN echo "/opt/gitlab/embedded/bin/runsvdir-start & EXTERNAL_URL='http://192.168.99.100' TERM=xterm && gitlab-ctl reconfigure\n\ntail -f /dev/null" > ./entrypoint.sh
RUN chmod +x ./entrypoint.sh

RUN sh ./entrypoint.sh


### Build container
# docker build -t unrealdir .

### Run
# docker run -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged unrealdir
