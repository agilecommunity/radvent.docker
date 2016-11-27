FROM ruby:2.1.5

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY src/Gemfile /usr/src/app/
COPY src/Gemfile.lock /usr/src/app/
RUN bundle install

COPY src /usr/src/app/

RUN    echo "gem 'pg'" >> Gemfile \
    && apt-get install -y libpq-dev \
    && bundle install

RUN apt-get update && apt-get install -y nodejs --no-install-recommends && rm -rf /var/lib/apt/lists/*

COPY config /usr/src/app/config/

RUN    mv vendor/assets/javascripts/* app/assets/javascripts/ \
    && mv vendor/assets/stylesheets/* app/assets/stylesheets/ \
    && bundle exec rake assets:precompile assets:clean

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
