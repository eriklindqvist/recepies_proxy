# Recepies Proxy
A simple docker-compose file to tie all the recipe services together

## Prerequisites
* Git (obviously)
* Docker
* Docker compose
* Go
* Node.js

## Getting started

### Get existing docker images
```
$ docker pull jwilder/nginx-proxy:alpine
$ docker pull mvertes/alpine-mongo
```

### Build backend image
```
$ cd ~/go/src/github.com/eriklindqvist/
$ git clone https://github.com/eriklindqvist/recepies_api.git
$ go get
$ ./build.sh
$ cd ..
```

### Build auth service
```
$ cd ~/go/src/github.com/eriklindqvist/
$ git clone https://github.com/eriklindqvist/recepies_auth.git
$ go get -d ./...
$ ./build.sh
$ cd ..
```

#### Generate keys
```
$ openssl genrsa -out certs/private.rsa 2048
$ openssl rsa -in certs/private.rsa -pubout > certs/public.rsa
```

### Build varsego static file server
```
$ git clone https://github.com/eriklindqvist/varsego.git
$ cd varsego
$ go get
$ ./build.sh
```

### Build frontend image
```
$ cd <WORKSPACE>
$ git clone https://github.com/eriklindqvist/recepies_ui.git
$ cd recipe_ui
$ npm install
$ ./build.sh
$ cd ..
```

### Fire it up
```
$ git clone https://github.com/eriklindqvist/recepies_proxy.git
$ cd recepies_proxy
$ docker-compose up
```

## Generate self signed SSL certificate
The provided key and cert will expire on 2018-12-27. To generate a new pair, execute the following command. This is for testing only. To run this in production, replace the certificates with keys signed by a trusted CA.

```
openssl req -x509 -newkey rsa:4096 -keyout recepies.local.key -out recepies.local.crt -days 365 -subj '/CN=recepies.local' -nodes
```
