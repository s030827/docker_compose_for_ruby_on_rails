# Initial Setup for rails 6 with docker-compose.
&nbsp;

```sh
$ git clone git@github.com:s030827/initial_docker_rails_6.git
```
- Create a .env file on the root folder.

```sh
$ touch .env
```

- Enter into rails_app folder and create rails project wit your preferences.

```sh
$ cd rails_app
$ rails new . --webpack --database=postgresql -T
```

> Obs:
> If you don't have rails installed you can run follows steps on the [docker-compose](https://docs.docker.com/compose/rails/) tutorial for rails.


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

- Edit your /rails_app/Gemfile and change the ruby version to the same that we defined on /rails_app/Dockerfile

- On the root folder run.

```sh
$ docker-compose build
$ docker-compose run app rails db:create db:migrate
$ docker-compose up
```