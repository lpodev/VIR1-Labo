# Step 2 - Create a Dockerfile for Java

* [Official Source](https://docs.docker.com/language/java/build-images/#create-a-dockerfile-for-java)

## Create your docker file

* [x] Change the directory to the app directory (we will use the same project [as for the previous step](step-1-run-the-project-outside-docker.md)).
* [x] Create an empty file named "Dockerfile"

```
[INPUT]
touch Dockerfile

[OUTPUT]
No output
```

* Using your IDE, add the following contents to the Dockerfile:

```
# syntax=docker/dockerfile:1

FROM eclipse-temurin:17-jdk-jammy
```

* [x] What is the purpose of the directive starting with "# syntax=docker..."

<!---->

* [Official documentation - Syntax directive](https://docs.docker.com/build/dockerfile/frontend/)

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
COPY src ./src
```

* Add the command responsible to run your application inside the Docker.

```
CMD ["./mvnw", "spring-boot:run"]
```

## Create a .dockerignore file

* [Official documentation - dockerignore](https://docs.docker.com/language/java/build-images/#create-a-dockerignore-file)

{% hint style="info" %}
To meet the good practice provided by Docker, we have to reduce the amount of data in the Docker build context. For this first lab, we will simply remove the directory containing the eventual outputs of MAVEN.
{% endhint %}

* [x] Create a .dockerignore file in the same directory as the Dockerfile.
* [x] Add the folder containing the MAVEN output.

## Build an image

{% hint style="info" %}
Best practices - docker tag naming convention:\
Read carefully [this doc](https://docs.docker.com/develop/dev-best-practices/) and deduce the right tag for your image.\
This [doc may also help you with tag samples](https://docs.docker.com/engine/reference/commandline/tag/).
{% endhint %}

* [x] Find the best tag for your image (this image is not intended for publication.)

```
java-lpo:dev
```

* [x] Build your first Docker image

Result Expected:

```docker
[INPUT]
docker build --tag <repository:tag>

[OUTPUT]
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
Successfully built <yourImageId>
Successfully tagged <yourRepository:yourTag>
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to dou
ble check and reset permissions for sensitive files and directories.

```

```
[INPUT]
docker build --tag java-lpo:dev ./

[OUTPUT]
[+] Building 0.8s (11/11) FINISHED
 => [internal] load .dockerignore                                                                                                                                            0.0s
 => => transferring context: 47B                                                                                                                                             0.0s
 => [internal] load build definition from Dockerfile                                                                                                                         0.0s
 => => transferring dockerfile: 234B                                                                                                                                         0.0s
 => [internal] load metadata for docker.io/library/eclipse-temurin:17-jdk-jammy                                                                                              0.7s
 => [internal] load build context                                                                                                                                            0.0s
 => => transferring context: 9.57kB                                                                                                                                          0.0s
 => [1/6] FROM docker.io/library/eclipse-temurin:17-jdk-jammy@sha256:13ff0fa4f9232f69b9f6e8a4cf86b7cb3a3783dbee06818aa5aee447159c1bc3                                        0.0s
 => CACHED [2/6] WORKDIR /app                                                                                                                                                0.0s
 => CACHED [3/6] COPY .mvn/ .mvn                                                                                                                                             0.0s
 => CACHED [4/6] COPY mvnw pom.xml ./                                                                                                                                        0.0s
 => CACHED [5/6] RUN ./mvnw dependency:resolve                                                                                                                               0.0s
 => CACHED [6/6] COPY src ./src                                                                                                                                              0.0s
 => exporting to image                                                                                                                                                       0.0s
 => => exporting layers                                                                                                                                                      0.0s
 => => writing image sha256:b6d10fb42b604c3d60fae4c332fa2dae6c969853e9b3e90bb274854f7ed279b2                                                                                 0.0s
 => => naming to docker.io/library/java-lpo:dev
```

## View local images

* [x] Using the "docker images" command, observe your images, and the associated tag.

### Result expected:

```
docker images
REPOSITORY        TAG            IMAGE ID       CREATED          SIZE
<yourRepository>  <yourTag>      910e5f0c8b1f   11 minutes ago   606MB
eclipse-temurin   17-jdk-jammy   56c7bc12ee6d   3 days ago       456MB
```

```
[INPUT]
docker images

[OUTPUT]
REPOSITORY     TAG       IMAGE ID       CREATED         SIZE
java-lpo       dev       b6d10fb42b60   5 minutes ago   602MB
```

## Using tags

* [x] Using the appropriate command, try to obtain this situation on your local machine:

```
[INPUT]
docker images

[OUTPUT]
REPOSITORY        TAG            IMAGE ID       CREATED       SIZE
petclinic         dev            323bdb488603   2 hours ago   606MB
petclinic         int            323bdb488603   2 hours ago   606MB
petclinic         prod           323bdb488603   2 hours ago   606MB
eclipse-temurin   17-jdk-jammy   56c7bc12ee6d   9 days ago    456MB
```

* [x] Is it a good idea to use tags like this to create different stages (dev, int, prod) ?

> The Docker tag helps maintain the build version to push the image to the Docker Hub**. The Docker Hub allows us to group images together based on name and tag.** Multiple Docker tags can point to a particular image. Basically, as in Git, Docker tags are similar to a specific commit. Docker tags are just an alias for an image ID.
>
> The tag's name must be an ASCII character string and may include lowercase and uppercase letters, digits, underscores, periods, and dashes. In addition, the tag names must not begin with a period or a dash, and they can only contain 128 characters.
>
> Source : [baeldung.com](https://www.baeldung.com/ops/docker-tag)

```
The Docker tag helps maintain the build version to push the image to the Docker Hub.
```

* [x] Using the appropriate command, update your local images and tags like this:

```
[INPUT]
docker images

[OUTPUT]
REPOSITORY          TAG              IMAGE ID       CREATED        SIZE
eclipse-petclinic   version1.0.dev   323bdb488603   18 hours ago   606MB
eclipse-temurin     17-jdk-jammy     56c7bc12ee6d   10 days ago    456MB
```

```
[INPUT]
build --tag petclinic:version1.0.dev ./

[OUTPUT]
[+] Building 0.8s (11/11) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                         0.0s
 => => transferring dockerfile: 234B                                                                                                                                         0.0s
 => [internal] load .dockerignore                                                                                                                                            0.0s
 => => transferring context: 47B                                                                                                                                             0.0s
 => [internal] load metadata for docker.io/library/eclipse-temurin:17-jdk-jammy                                                                                              0.8s
 => [1/6] FROM docker.io/library/eclipse-temurin:17-jdk-jammy@sha256:13ff0fa4f9232f69b9f6e8a4cf86b7cb3a3783dbee06818aa5aee447159c1bc3                                        0.0s
 => [internal] load build context                                                                                                                                            0.0s
 => => transferring context: 9.57kB                                                                                                                                          0.0s
 => CACHED [2/6] WORKDIR /app                                                                                                                                                0.0s
 => CACHED [3/6] COPY .mvn/ .mvn                                                                                                                                             0.0s
 => CACHED [4/6] COPY mvnw pom.xml ./                                                                                                                                        0.0s
 => CACHED [5/6] RUN ./mvnw dependency:resolve                                                                                                                               0.0s
 => CACHED [6/6] COPY src ./src                                                                                                                                              0.0s
 => exporting to image                                                                                                                                                       0.0s
 => => exporting layers                                                                                                                                                      0.0s
 => => writing image sha256:b6d10fb42b604c3d60fae4c332fa2dae6c969853e9b3e90bb274854f7ed279b2                                                                                 0.0s
 => => naming to docker.io/library/petclinic:version1.0.dev
```
