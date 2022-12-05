# keycloak + web + nginx(ssl)

## web

```
docker exec demo /opt/jboss/wildfly/bin/add-user.sh admin admin --silent
```

## security

```
# CA
openssl genrsa -out CAcert-key.pem 2048
openssl req -new -key CAcert-key.pem -out CAcert.csr
openssl x509 -req -days 3650 -in CAcert.csr -signkey CAcert-key.pem -out CAcert.pem

# Server
openssl genrsa -out server-key.pem 2048
openssl req -new -key server-key.pem -out server-cert.csr
openssl x509 -req -days 3650 -CAcreateserial -in server-cert.csr -CA CAcert.pem -CAkey CAcert-key.pem -out server-cert.pem

# trust store
keytool -import -keystore trust.jks -file CAcert.pem -alias caroot
keytool –import –keystore trust.jks –file server-cert.pem –alias server
```
