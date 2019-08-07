FROM ubuntu:16.04

ARG GITLAB_OMNIBUS_CONFIG="external_url 'http://192.168.99.100/'; gitlab_rails['lfs_enabled'] = true; grafana['enable'] = false; gitlab_rails['gitlab_shell_ssh_port'] = 23;"

RUN apt-get update && apt-get upgrade -y && apt-get install ca-certificates openssh-server wget postfix -y

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && chmod 777 script.deb.sh && ./script.deb.sh && apt-get install gitlab-ce -y

EXPOSE 443 80 22

ENTRYPOINT [ "gitlab" ]

# RUN echo "/opt/gitlab/embedded/bin/runsvdir-start & gitlab-ctl reconfigure\n\ntail -f /dev/null" > ./entrypoint.sh
# RUN chmod +x ./entrypoint.sh
# RUN chmod +t /tmp

# RUN sh ./entrypoint.sh

### Build container
# docker build -t unrealdir .

### Run
# docker run -d -h 192.168.99.100 -p 192.168.99.100:443:443 -p 192.168.99.100:80:80 -p 192.168.99.100:23:22 --name gitlab --restart always -v /srv/gitlab/config:/etc/gitlab -v /srv/gitlab/logs:/var/log/gitlab -v /srv/gitlab/data:/var/opt/gitlab unrealdir
