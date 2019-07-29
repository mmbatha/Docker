FROM ubuntu:16.04

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends wget openssh-server ca-certificates gnupg postfix

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
RUN chmod 777 script.deb.sh

RUN ./script.deb.sh
RUN EXTERNAL_URL="http://192.168.99.100:8080/" apt-get install gitlab-ce=11.11.2-ce.0 -y
RUN echo "external_url 'http://192.168.99.100:8080/';" > /etc/gitlab/gitlab.rb

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 443 80 22
ENTRYPOINT gitlab-ctl reconfigure & /opt/gitlab/embedded/bin/runsvdir-start

### Build container
# docker build -t ex03 . > output.txt

### Run
# docker run -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03
