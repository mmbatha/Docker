FROM ubuntu:16.04

RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
      ca-certificates \
      openssh-server \
      curl \
      postfix

WORKDIR /
RUN curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh

RUN bash script.deb.sh

RUN apt-get update && EXTERNAL_URL="http://gitlab.example.com" apt-get install -yq gitlab-ce

# Missing Time Zone Data /usr/share/zoneinfo
# https://gitlab.com/gitlab-org/omnibus-gitlab/issues/2229
RUN apt update && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22 80

RUN echo "/opt/gitlab/embedded/bin/runsvdir-start & EXTERNAL_URL='http://192.168.99.100' TERM=xterm && gitlab-ctl reconfigure\n\ntail -f /dev/null" > ./entrypoint.sh
RUN chmod +x ./entrypoint.sh

CMD [ "bash", "./entrypoint.sh" ]


### Build container
# docker build -t fakedir .

### Run
# docker run -it --rm -p 8080:80 -p 8022:22 --privileged fakedir
