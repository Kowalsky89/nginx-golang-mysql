```
.
├── backend
│   ├── Dockerfile
│   ├── go.mod
│   └── main.go
├── db
│   └── password.txt
├── docker-compose.yaml
├── proxy
│   ├── conf
│   └── Dockerfile
└── README.md
```
```
$ docker-compose up -d
Creating network "nginx-golang-mysql_default" with the default driver
Building backend
Step 1/8 : FROM golang:1.13-alpine AS build
1.13-alpine: Pulling from library/golang
...
Successfully built 5f7c899f9b49
Successfully tagged nginx-golang-mysql_proxy:latest
WARNING: Image for service proxy was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating nginx-golang-mysql_db_1 ... done
Creating nginx-golang-mysql_backend_1 ... done
Creating nginx-golang-mysql_proxy_1   ... done
```
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
8906b14c5ad1        nginx-golang-mysql_proxy     "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes        0.0.0.0:80->80/tcp    nginx-golang-mysq
l_proxy_1
13e0e0a7715a        nginx-golang-mysql_backend   "/server"                2 minutes ago       Up 2 minutes        8000/tcp              nginx-golang-mysq
l_backend_1
ca8c5975d205        mysql:5.7                    "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        3306/tcp, 33060/tcp   nginx-golang-mysq
l_db_1
```
```
$ curl localhost:80
["Blog post #0","Blog post #1","Blog post #2","Blog post #3","Blog post #4"]
```
```
$ docker-compose down
```
