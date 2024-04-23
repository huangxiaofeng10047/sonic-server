```
docker run -itd -p 636:636 -p 389:389 --restart=always --name openldap \
-v $PWD/mydata/ldap/data:/var/lib/ldap \
-v $PWD/mydata/ldap/config:/etc/ldap/slapd.d \
--env LDAP_ORGANISATION="dra-m" \
--env LDAP_DOMAIN="dra-m.com" \
--env LDAP_ADMIN_PASSWORD="sonic" \
--ulimit nproc=1024 \
--detach osixia/openldap --copy-service
```

```
docker run \
-d \
--privileged \
-p 8989:80 \
--name myldapadmin \
--env PHPLDAPADMIN_HTTPS=false \
--env PHPLDAPADMIN_LDAP_HOSTS=172.31.21.37 \
--detach osixia/phpldapadmin

```
TODO
上面的不可以用
重新写
```
docker run \
-p 389:389 \
-p 636:636 \
--name de-ldap \
--network bridge \
--hostname deldap.com \
--env LDAP_ORGANISATION="deldap" \
--env LDAP_DOMAIN="deldap.com" \
--env LDAP_ADMIN_PASSWORD="123456" \
--volume /opt/ldap/certificates:/container/service/slapd/assets/certs \
--env LDAP_TLS_CRT_FILENAME=ldap.crt \
--env LDAP_TLS_KEY_FILENAME=ldap.key \
--env LDAP_TLS_CA_CRT_FILENAME=ca.crt \
--detach osixia/openldap

docker run \
-d \
--privileged \
-p 8989:80 \
--name myldapadmin \
--env PHPLDAPADMIN_HTTPS=false \
--env PHPLDAPADMIN_LDAP_HOSTS=10.7.202.35 \
--detach osixia/phpldapadmin

```