FROM			ruby:latest

LABEL			Author="Monde MBATHA <mmbatha@student.42.fr>" \
				Description="Ruby-based container that runs a sample Rails application" \
				License="MIT License 2.0" \
				Usage="docker run -it --rm -p [HOST_PORT]:3000 rails"

RUN				apt-get update -y && apt-get upgrade -y && apt-get install nodejs yarn -y && gem install rails && mkdir -p /opt/app

ONBUILD WORKDIR	/opt/app

ONBUILD ADD		. /opt/app

ONBUILD EXPOSE	3000

ONBUILD RUN		bundle install --without production && rails db:migrate && rails test

# docker build -t ft-rails:on-build .
# git clone https://github.com/mhartl/hello_app_original.git sample_app
# cd sample_app
# echo "FROM\tft-rails:on-build\n\nEXPOSE\t3000\n\nCMD\t\t[\"rails\", \"s\", \"-b\", \"0.0.0.0\", \"-p\", \"3000\"]" > Dockerfile
## set check_yarn_integrity to 'false' in sample_app/config/webpacker.yml
## comment out last line in sample_app/Gemfile
# docker build -t rails .
# docker run -it --rm -p 3000:3000 rails
# Browse to http://192.168.99.100:3000/
