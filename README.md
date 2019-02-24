# Taiwan Stock/Future Exchange Data Analysis
- `twsfex-main` is main project of this service.
- Main project includes `job-queue`, `scheduler` and `docker-compose.yml` to build the whole service.
- Using Golang and Docker.

## Installation
### Test by Docker Compose
```console
>docker-compose up -d
```
After completion, we could use following commands to check:

Check volume:
```console
>docker volume ls
```
We should find something like this:
```console
DRIVER              VOLUME NAME
local               twsfex-main_mongo-config
local               twsfex-main_mongo-data
```

Check network:
```console
>docker network ls
```
We should find this network:
```console
NETWORK ID          NAME                         DRIVER              SCOPE
dc86de677bcf        twsfex-main_twsfex-backend   bridge              local
```

Also, we could check the status of containers:
```console
>docker container ls
```
And the status should be `Up...`
```console
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                      NAMES
f31e562a9d5a        twsfex-main_mongo-api   "./app"                  9 minutes ago       Up 9 minutes        0.0.0.0:8080->8080/tcp     twsfex-main_mongo-api_1
2af2fefb9aa5        mongo-express:latest    "tini -- /docker-ent…"   9 minutes ago       Up 9 minutes        0.0.0.0:8081->8081/tcp     twsfex-main_mongo-express_1
cb5bec0156ca        mongo:latest            "docker-entrypoint.s…"   9 minutes ago       Up 9 minutes        0.0.0.0:27017->27017/tcp   twsfex-main_mongo_1
```

At last, we could test the `mongodb` through `mongo-express`. Enter http://127.0.0.1:8081/ in the browser and we should see something like this picture:
![mongo-express screen shot](https://github.com/neofelisho/twsfex-main/blob/master/mongo-express.png)

And enter http://127.0.0.1:8080/ could test the `mongo-api`. If everythinig is alright, `"{test: ok}"` would be printed on the screen.

### Deploy to Docker Machine(s) by Docker Swarm

## TODO
1. Establish job-queue.
2. Build a scheduler by Golang.
3. Build a data analyzer by Golang.
4. Replace RESTful by gRPC.