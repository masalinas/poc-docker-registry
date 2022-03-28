# Description
Poc local image docker registry

## Start docker resigtry
Start docker registry version 2 with authentication

Firts create credentials

```shell
mkdir auth
docker run --entrypoint htpasswd httpd:2 -Bbn admin password > auth/htpasswd
```

Second start registry service
```shell
docker run -d -p 5000:5000 --name registry -v "$(pwd)"/auth:/auth -e REGISTRY_AUTH=htpasswd -e REGISTRY_AUTH_HTPASSWD_REALM="Registry Realm" -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd registry:2
```

## Login to the Registry
```shell
docker login localhost:5000
```

## Tag a image
```shell
docker tag nginx localhost:5000/nginx
```

## Push image
```shell
docker push localhost:5000/nginx
```

## list images
```shell
curl -X GET -u admin:password http://localhost:5000/v2/_catalog
```

## pull image
docker pull localhost:5000/nginx
