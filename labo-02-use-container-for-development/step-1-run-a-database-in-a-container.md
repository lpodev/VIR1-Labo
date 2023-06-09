# Step 1 - Run a database in a container

* [Official Source](https://docs.docker.com/language/java/develop/#run-a-database-in-a-container)

## Prerequisites

Take the time to become familiar with the concept of volumes before carrying out this lab : [Docker and Volumes](https://docs.docker.com/storage/volumes/).

## Setup Database Docker dependencies

### Add volumes

Let's create both volumes, one for the data, and another one for the db config.

* [x] Create one volume for the MySQL data (tag name : mysql_data)

```
[INPUT]
docker volume create mysql_data

[OUTPUT]
mysql_data
```

* [x] Create a second volume for the MySQL configuration (tag name : mysql_config)

```
[INPUT]
docker volume create mysql_config

[OUTPUT]
mysql_config
```

* [x] List the volumes

```
[INPUT]
docker volume ls  

[OUTPUT]
DRIVER    VOLUME NAME
local     mysql_config
local     mysql_data
```

### Network Creation

Let's create a user-defined bridge network enabling our application and our database to talk to each other.

* [x] Create the network

```
[INPUT]
docker network create mysqlnet

[OUTPUT]
71814d243c0ecac7c337bbc2a2a93fd5d4abd9365475b61b66c4349506041599
```

* [x] List the networks

```
[INPUT]
docker network ls

[OUTPUT]
NETWORK ID     NAME       DRIVER    SCOPE
8a3fe1df2b00   bridge     bridge    local
f81f31f8f218   host       host      local
71814d243c0e   mysqlnet   bridge    local
a3768e021991   none       null      local
```

### Run MySQL

Let's run MySQL in a container and attach to the volumes and network we created above.

{% hint style="info" %}
To avoid this message:
```
docker: Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:3306 -> 0.0.0.0:0: listen tcp 0.0.0.0:3306: bind: Only one usage of each socket address (protocol/network address/port) is normally permitted.
```
Check your host ports and do no try to forward one of them that is already is use.
{% endhint %}

```
[INPUT]
docker run -it --rm -d -v mysql_data:/var/lib/mysql \
-v mysql_config:/etc/mysql/conf.d \
--network mysqlnet \
--name mysqlserver \
-e MYSQL_USER=petclinic -e MYSQL_PASSWORD=petclinic \
-e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=petclinic \
-p 3308:3306 mysql:8.0

[OUTPUT]
fd1e3908730051aa29c2f8766bedf9558ed17b98b35cafd8edac4e9f50ea752e
```

* [x] List all containers (all states)

```
[INPUT]
docker ps -a --format "table {{.Image}}\t{{.Ports}}\t{{.Names}}"

[OUTPUT]
IMAGE                          PORTS                               NAMES
mysql:8.0                      33060/tcp, 0.0.0.0:3308->3306/tcp   mysqlserver
petclinic-app:version1.0.dev   0.0.0.0:8080->8080/tcp              silly_antonelli
```

### Update our Dockerfile to activate MySQL

Currently H2 is used on our Petclinic Container. We need to switch on MySQL.

* [x] Add this command to your Dockerfile, in the right place.

```
CMD ["./mvnw", "spring-boot:run", "-Dspring-boot.run.profiles=mysql"]
```

* [x] If you run both docker, the application server will not able to talk with the dbserver... any idea why ?

```
If you run both the Docker containers for the application server and the database server separately, they won't be able to communicate because they are not connected to the same network. To allow communication between the containers, you need to ensure that both containers are attached to the same network.
```

* [x] Let's build our image

```
[INPUT]
docker build --tag eclipse-petclinic:version1.1.dev .

[OUTPUT]
REPOSITORY          TAG              IMAGE ID       CREATED       SIZE
eclipse-petclinic   version1.1.dev   c81b4edc2ea9   2 hours ago   611MB
mysql               8.0              fe893ca74649   11 days ago   592MB
springboot-lpo      dev              7871880f62a8   2 weeks ago   602MB
springboot-lpo      int              7871880f62a8   2 weeks ago   602MB
springboot-lpo      prod             7871880f62a8   2 weeks ago   602MB
petclinic-app       version1.0.dev   7871880f62a8   2 weeks ago   602MB
```

* [x] Test your application

```
[INPUT]
docker start silly_antonelli


[INPUT]
//Call the vets route
curl --request GET \
    --url http://localhost:8080/vets \
    --header 'content-type: application/json'

[OUTPUT]
{"vetList":[{"id":1,"firstName":"James","lastName":"Carter","specialties":[],"nrOfSpecialties":0,"new":false},{"id":2,"firstName":"Helen","lastName":"Leary","specialties":[{"id":1,"name":"radiology","new":false}],"nrOfSpecialties":1,"new":false},{"id":3,"firstName":"Linda","lastName":"Douglas","specialties":[{"id":3,"name":"dentistry","new":false},{"id":2,"name":"surgery","new":false}],"nrOfSpecialties":2,"new":false},{"id":4,"firstName":"Rafael","lastName":"Ortega","specialties":[{"id":2,"name":"surgery","new":false}],"nrOfSpecialties":1,"new":false},{"id":5,"firstName":"Henry","lastName":"Stevens","specialties":[{"id":1,"name":"radiology","new":false}],"nrOfSpecialties":1,"new":false},{"id":6,"firstName":"Sharon","lastName":"Jenkins","specialties":[],"nrOfSpecialties":0,"new":false}]}%
```
