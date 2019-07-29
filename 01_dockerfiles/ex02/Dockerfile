FROM ruby
RUN apt-get update && apt-get upgrade -y && gem install rails && apt-get install nodejs apt-utils --no-install-recommends -y
ONBUILD COPY . /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install && rails db:migrate && rails db:seed
