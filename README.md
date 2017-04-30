# Docker Ulbora User Service
- 1.0.2, latest[ (Dockerfile)](https://github.com/Ulbora/docker_ulbora_user_service/blob/master/Dockerfile)

This is Docker Ulbora User Micro Service running on Alpine


# Running
```
docker run -p some-port:8080 --name ulbora-user-service \
--env DATABASE_USER_NAME=some-user-name \
--env DATABASE_USER_PASSWORD=some-user-password \
--env DATABASE_NAME=some-db-name \
--env DATABASE_POOL_SIZE=pool-size \
--env OAUTH2_VALIDATION_URI=oauth2-server \
--env PORT=8080 \
--link some-mysql-container-name:mysql -it  \
ulboralabs/userservice sh
```
#### or as a daemon (suggested)
```
docker run -p some-port:8080 --name ulbora-user-service \
--env DATABASE_USER_NAME=some-user-name \
--env DATABASE_USER_PASSWORD=some-user-password \
--env DATABASE_NAME=some-db-name \
--env DATABASE_POOL_SIZE=pool-size \
--env OAUTH2_VALIDATION_URI=oauth2-server \
--env PORT=8080 \
--link some-mysql-container-name:mysql -d  \
ulboralabs/userservice sh
```
# Note
### The link to your mysql container should always end with :mysql as shown above
```
--link some-mysql-container-name:mysql 
```
The :mysql is an alias that produces an environment variable named MYSQL_PORT_3306_TCP_ADDR inside the web container.
If :mysql were to be changed to :mysqldb, then the environment variable would be named MYSQLDB_PORT_3306_TCP_ADDR and 
the User Micro Service would not connect the the mysql database. The User Micro Service needs the environment variable to be 
named MYSQL_PORT_3306_TCP_ADDR.

### Ports on the host machine should be different for each container
#### Example: 
#### -p host-port-number:container-port-number
```
-p 3001:8080 
-p 3002:8080 
-p 3003:8080
```

# Connect to running instance
```
docker exec -it ulboralabs/userservice sh
```

