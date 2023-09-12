Fluxo: [notes](https://www.notion.so/Nivelamento-e90fad7d5de04f9bb2a91568932c9e01?pvs=4#1bccacb7bc8d42d289fe8824cf97f988)

Docker-compose
```docker
version: '3'

services:
  webserver-go:
    container_name: webserver-go
    hostname: webserver-go
    build:
      context: services/webserver
      dockerfile: Dockerfile
      target: development
    environment:
      - DEVELOPER_NAME=lucas
    ports:
      - 8080:8080
```

Subindo container

> `dc` é um alias para docker-compose
> 

```bash
ubunto in leveling/docker/docker-compose 
➜  dc up -d     
[+] Building 15.8s (10/10) FINISHED                                                               docker:default
 => [webserver-go internal] load build definition from Dockerfile                                           0.1s
 => => transferring dockerfile: 272B                                                                        0.0s
 => [webserver-go internal] load .dockerignore                                                              0.1s
 => => transferring context: 2B                                                                             0.0s
 => [webserver-go internal] load metadata for docker.io/library/golang:latest                               1.7s
 => [webserver-go auth] library/golang:pull token for registry-1.docker.io                                  0.0s
 => CACHED [webserver-go 1/4] FROM docker.io/library/golang:latest@sha256:d2aad22fc6f1017aa568d980b15d0067  0.0s
 => [webserver-go internal] load build context                                                              0.0s
 => => transferring context: 609B                                                                           0.0s
 => [webserver-go 2/4] RUN go install github.com/githubnemo/CompileDaemon@latest                           13.6s
 => [webserver-go 3/4] COPY . /usr/src/app                                                                  0.1s
 => [webserver-go 4/4] WORKDIR /usr/src/app                                                                 0.1s
 => [webserver-go] exporting to image                                                                       0.3s 
 => => exporting layers                                                                                     0.3s 
 => => writing image sha256:8ea64e3d1faaefc833607f07a75d4989894c85d54b0d9bb464995d6fbe626aab                0.0s 
 => => naming to docker.io/library/docker-compose-webserver-go                                              0.0s 
[+] Running 2/2
 ✔ Network docker-compose_default  Created                                                                  0.1s 
 ✔ Container webserver-go          Started                                                                  0.0s 
ubunto in leveling/docker/docker-compose took 16,2s 
➜  dc ps -a
NAME                IMAGE                         COMMAND                  SERVICE             CREATED             STATUS              PORTS
webserver-go        docker-compose-webserver-go   "/bin/sh -c 'Compile…"   webserver-go        3 seconds ago       Up 2 seconds        0.0.0.0:8080->8080/tcp, :::8080->8080/tcp
```

Saída
```bash
➜  curl localhost:8080
Hello, lucas
```