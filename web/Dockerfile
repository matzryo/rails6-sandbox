FROM ruby:2.7 as base
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs
RUN mkdir /todo_app
WORKDIR /todo_app
COPY Gemfile /todo_app/Gemfile
COPY Gemfile.lock /todo_app/Gemfile.lock
RUN bundle install
COPY . /todo_app

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]

FROM base as dev