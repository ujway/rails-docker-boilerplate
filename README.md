# Rails Docker Boilerplate

## System Configuration

| Item                          | Content                                      |
|------------------------------ |----------------------------------------------|
| Framework                     | Ruby on Rails 5.2.0                          |
| Ruby Version                  | 2.5.1                                        |
| Database                      | MySQL 5.7.22                                 |
| API Document                  | Swagger(OpenAPI 2.0)                         |
| Required Middleware           | Docker version 18.03.0-ce                    |
| Bug report / feature requests | [GitHub Issue](https://github.com/ujway/rails-docker-boilerplate/issues) |

## Getting Started

```bash
# Clone
https://github.com/ujway/rails-docker-boilerplate.git
cd rails-docker-boilerplate

# Docker container create, install bundle and run a rails server
docker -v # out> Docker version 17.12.0-ce, build c97c6d6
docker-compose build
docker-compose up -d

# Setup rails database
docker-compose exec web ruby -v # out> ruby 2.5.0p0 ...
docker-compose exec web rails -v # out> Rails 5.1.5
docker-compose exec web rails db:create
docker-compose exec web rails db:migrate

#### Remove all containers and images defined in docker-compose
# docker-compose down -v --rmi all
```

example:

1. Rails
- http://localhost:4567
  - DBのホスト: localhost:4568
  
2. Swagger UI（./doc/swagger.yamlの内容を表示）
- http://localhost:4569/

## Development Memos
`docker-compose exec web [Command]`でコンテナ外でコマンドが実行可能ですが、  
`docker-compose exec -it web bash`でコンテナ内部に入ってコマンドを実行することもできます。  
`docker-compose exec web`は`docker exec rails_api_web`として実行可能です。

### Docker
- 起動中のdockerコンテナのシェルに入る
    - ``` docker-compose exec -it web bash ```
- dockerコンテナでコマンドを実行する
    - ``` docker-compose exec web [Command] ```

### Rails
- Model or Controllerを作成する
    - ``` docker-compose exec web rails g [model|controller] [ModelName|ControllerName]```を実行する
- Migrationを作成する
    - ``` docker-compose exec web rails g migration [MigrationName] ```を実行する
    - 生成された``` db/migrate/{yyyymmddhhmmss}_{migration_name}.rb ```にchange/up/downを記載する
    - ``` docker-compose exec web rails db:migrate ```を実行する
- Migrationをリセットする
    - ``` docker-compose exec web rails db:migrate:reset```を実行する

### API Definition
- Swaggerの定義を編集する
    - ``` doc/swagger.yaml ```

## License
This software is released under the MIT License, see LICENSE.txt.
