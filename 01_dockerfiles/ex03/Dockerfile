FROM	ubuntu:16.04

LABEL	Author="Monde MBATHA <mmbatha@student.42.fr>" \
		Description="Ubuntu-based container that installs and runs Gitlab" \
		License="MIT License 2.0" \
		Usage="docker run -it --rm 80:80 -p 21:22 --privileged ex03"

RUN apt-get update -q && DEBIAN_FRONTEND=noninteractive apt-get install -yq  ca-certificates openssh-server curl postfix && curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && bash script.deb.sh && apt-get update && EXTERNAL_URL="http://192.168.99.115/" apt-get install -yq  gitlab-ce && apt-get update && apt-get install -y tzdata && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22 80

RUN echo "/opt/gitlab/embedded/bin/runsvdir-start& EXTERNAL_URL=\"0.0.0.0\" && gitlab-ctl reconfigure\n\ntail -f /dev/null" > /entrypoint.sh && chmod +x /entrypoint.sh

CMD [ "bash", "/entrypoint.sh" ]

### Build container
# docker build -t ex03 .

### Run container
# docker run -it --rm 80:80 -p 21:22 --privileged ex03

### Run original container
# docker run -d --privileged -h 192.168.99.115 -e GITLAB_OMNIBUS_CONFIG="external_url 'http://192.168.99.115/'; gitlab_rails['lfs_enabled'] = true; grafana['enable'] = false; gitlab_rails['gitlab_shell_ssh_port'] = 23;" -p 192.168.99.115:443:443 -p 192.168.99.115:80:80 -p 192.168.99.115:23:23 --name gitlab --restart always -v /srv/gitlab/config:/etc/gitlab -v /srv/gitlab/logs:/var/log/gitlab -v /srv/gitlab/data:/var/opt/gitlab -v /srv/gitlab/logs/reconfigure:/var/log/gitlab/reconfigure gitlab/gitlab-ce:11.10.8-ce.0
