FROM ruby:2.6.6-alpine3.11

# Minimal requirements to run a Rails app
RUN apk add --no-cache --update build-base \
    linux-headers \
    git \
    postgresql-dev \
    nodejs \
    yarn \
    tzdata \
    curl \
    imagemagick

ENV APP_PATH /usr/src/app

# Different layer for gems installation
WORKDIR $APP_PATH
ADD rails_app/Gemfile $APP_PATH
ADD rails_app/Gemfile.lock $APP_PATH
RUN gem list bundler
RUN gem install bundler
RUN gem list bundler
RUN bundle install
RUN RAILS_ENV=${RAILS_ENV}

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh

# Copy the application into the container
COPY rails_app $APP_PATH

ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000
CMD [ "bundle", "exec", "puma", "-C", "config/puma.rb" ]