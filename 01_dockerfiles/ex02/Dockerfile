FROM ruby
RUN apt-get update && apt-get upgrade -y && gem install rails && apt-get install nodejs -y
ONBUILD COPY . /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install && rails db:migrate && rails db:seed