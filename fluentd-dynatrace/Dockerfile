FROM fluent/fluentd:v1.13-1

USER root

COPY Gemfile* /fluentd/

RUN apk add --no-cache --update --virtual .build-deps build-base ruby-dev \
    && gem install bundler --version 2.2.6 \
    && bundle config silence_root_warning true \
    && bundle config set path '/fluentd/vendor/bundle' \
    && bundle install --gemfile=/fluentd/Gemfile \
    && gem sources --clear-all \
    && apk del .build-deps \
    && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

# Copy plugins
COPY plugins /fluentd/plugins/
COPY entrypoint.sh /bin/
