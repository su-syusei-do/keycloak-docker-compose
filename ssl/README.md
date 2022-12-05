# keycloak + web + nginx(ssl)

## web

```
docker exec demo /opt/jboss/wildfly/bin/add-user.sh admin admin --silent
```

## security

```
# 秘密鍵
sudo openssl genrsa -out ./nginx/ssl/server.key 2048

# CSR
sudo openssl req -new -key ./nginx/ssl/server.key -out ./nginx/ssl/server.csr

# CRT
sudo openssl x509 -days 3650 -req -signkey ./nginx/ssl/server.key -in ./nginx/ssl/server.csr -out ./nginx/ssl/server.crt
```
