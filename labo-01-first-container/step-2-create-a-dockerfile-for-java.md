# Step 2 - Create a Dockerfile for Java

* [Official Source](https://docs.docker.com/language/java/build-images/#create-a-dockerfile-for-java)

## Create your docker file

* [x] Change the directory to the app directory (we will use the same project [as for the previous step](step-1-run-the-project-outside-docker.md)).
* [x] Create an empty file named "Dockerfile"

```
[INPUT]
mkdir app
touch app/Dockerfile

[OUTPUT]
No output
```

* Using your IDE, add the following contents to the Dockerfile:

```
# synthax=docker/dockerfile:1

FROM eclipse-temurin:17-jdk-jammy
```

* [ ] What is the purpose of the directive starting with "# syntax=docker..."

<!---->

* [Official documentation - Synthax directive](https://docs.docker.com/build/dockerfile/frontend/)

```
This defines the location of the Dockerfile syntax that is used to build the Dockerfile.
```

* [x] Is the docker image suitable for a production environment?

```
Yes, because the dockerfile:1 contains the latest stable release of the version 1 syntax, and receives both “minor” and “patch” updates for the version 1 release cycle.
```

### Dependencies resolution and first app build

* [x] Set the image's working directory by adding this command line:

```
WORKDIR /app
```

* [x] Before we can resolve dependencies with _MAVEN,_ we need to get the _MAVEN_ wrapper and your pom.xml file into your image.

```
COPY .mvn/ .mvn
COPY mvnw pom.xml ./
```

* [x] Let's use _MAVEN_ to resolve the dependencies.

```
RUN ./mvnw dependency:resolve
```

* [x] How is it possible to resolve the dependencies when the source code is not available at this point in the process?

```
By declaring dependencies in a configuration file and using a package manager to install them, the Docker image can be built without needing access to the source code. However, it's important to note that if the dependencies change frequently, it may be necessary to rebuild the Docker image more often to ensure that it always contains the latest dependencies.
```

* Add the command able to provide (copy) your source code to the image.

```
FROM some-base-image
COPY . /app
```

* Add the command responsible to run your application inside the Docker.

```
docker build -t my-image .
```

## Create a .dockerignore file

* [Official documentation - dockerignore](https://docs.docker.com/language/java/build-images/#create-a-dockerignore-file)

{% hint style="info" %}
To meet the good practice provided by Docker, we have to reduce the amount of data in the Docker build context. For this first lab, we will simply remove the directory containing the eventual outputs of MAVEN.
{% endhint %}

* [ ] Create a .dockerignore file in the same directory as the Dockerfile.
* [ ] Add the folder containing the MAVEN output.

## Build an image

{% hint style="info" %}
Best practices - docker tag naming convention:\
Read carefully [this doc](https://docs.docker.com/develop/dev-best-practices/) and deduce the right tag for your image.\
This [doc may also help you with tag samples](https://docs.docker.com/engine/reference/commandline/tag/).
{% endhint %}

* [ ] Find the best tag for your image (this image is not intended for publication.)

```
//TODO
```

* [ ] Build your first Docker image

Result Expected:

```
docker build --tag <yourTag>
Sending build context to Docker daemon   9.92MB
Step 1/7 : FROM eclipse-temurin:17-jdk-jammy
 ---> 56c7bc12ee6d
 ---> Using cache
 ---> b4854585fa31
Step 3/7 : COPY .mvn/ .mvn
 ---> Using cache
 ---> b72a055eb5f8
Step 4/7 : COPY mvnw pom.xml ./
 ---> Using cache
 ---> ae3709e4bfb7
Step 5/7 : RUN ./mvnw dependency:resolve
 ---> Using cache
 ---> e62d33f55785
Step 6/7 : COPY src ./src
 ---> Using cache
 ---> b926a101aec1
Step 7/7 : CMD ["./mvnw", "spring-boot:run"]
 ---> Using cache
 ---> 910e5f0c8b1f
Successfully built 910e5f0c8b1f
Successfully tagged java-docker:dev
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to dou
ble check and reset permissions for sensitive files and directories.

```

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```

### View local images

* [ ] Using the "docker images" command, observe your images, and the associates tag.

Result expected:\


```
docker images
REPOSITORY        TAG            IMAGE ID       CREATED          SIZE
java-docker       <yourTag>      910e5f0c8b1f   11 minutes ago   606MB
eclipse-temurin   17-jdk-jammy   56c7bc12ee6d   3 days ago       456MB
```

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```
