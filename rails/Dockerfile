FROM ruby:2.4

RUN apt-get update -qq && apt-get install -y build-essential

# for postgres
RUN apt-get install -y libpq-dev

# for nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev

# for capybara-webkit
RUN apt-get install -y libqt4-webkit libqt4-dev xvfb

# for a JS runtime
RUN apt-get install -y nodejs

ENV APP_HOME /rails
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

# Install comfy

COPY Gemfile $APP_HOME/Gemfile

RUN bundle install
RUN rails new sofa
COPY database.yml $APP_HOME/sofa/config
RUN cd sofa && rails generate comfy:cms

COPY db_init /bin
RUN chmod 555 /bin/db_init

RUN echo "Comfy::Cms::Site.create!(identifier: 'default-site', hostname: 'change-me')" >> $APP_HOME/sofa/db/seeds.rb
WORKDIR $APP_HOME/sofa
