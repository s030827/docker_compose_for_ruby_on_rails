# Initial Setup for rails 6 with docker-compose.

&nbsp;

```sh
$ git clone git@github.com:s030827/docker_compose_for_ruby_on_rails.git name_of_your_application
```

- Create a .env file on the root folder.

```sh
$ touch .env
```

- Enter into name_of_your_application folder and create rails project with your preferences.


```sh
$ cd name_of_your_application
$ docker-compose run app rails new . --force --no-deps --database=postgresql -T -C
```

- Edit the file /rails_app/config/database.yml

```
  default: &default
    adapter: postgresql
    encoding: UTF8
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: postgres
    password: <%= ENV['KEY_POSTGRES'] %>
    host: db

  development:
    <<: *default
    database: my_rails_app_name_dev

  test:
    <<: *default
    database: my_rails_app_name_test

  production:
    <<: *default
    database: my_rails_app_name_production
```

- Edit the file .env

```sh
  RAILS_ENV=development
  KEY_POSTGRES=UEAjc3N3b3JkOQo=
```

- On the root folder run.

```sh
$ docker-compose build
$ docker-compose run app rails db:create db:migrate
$ docker-compose up
```

> Obs:

- [docker-compose](https://docs.docker.com/compose/rails/) tutorial for rails.
- For specifying the Rails version edit the file rails_app/Gemfile.
- For specifying the Ruby version edit the file rails_app/Dockerfile.
