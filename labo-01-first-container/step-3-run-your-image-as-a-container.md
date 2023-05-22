# Step 3 - Run your image as a container

* [Official Source](https://docs.docker.com/language/java/run-containers/)

<!---->

* [x] Run your "petclinic" docker based on the image created in the previous step.
  * [ ] We should access to your application using the http standard port.

Result expected:

{% hint style="info" %}
Linux user, change ^ by ' to execute multi lines commands.
{% endhint %}

```
[INPUT]
curl --request GET \
--url http://localhost/actuator/health \
--header 'content-type: application/json'

[OUTPUT]
{"status":"UP"}

//disregard the message curl: (6) Could not resolve host: application
```

* [x] List all Dockers currently running on your local environment. Observe the port forwarding for your "petclinic" docker.

```
[INPUT]
docker container ls

[OUTPUT]
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                    NAMES
81adc5d1f02b   petclinic:prod   "./mvnw spring-boot:…"   4 minutes ago   Up 4 minutes   0.0.0.0:8080->8080/tcp   magical_bhaskara

```

* [x] Stop your "petclinic" docker

```
[INPUT]
ctrl+c in terminal

[OUTPUT]
2023-05-15T09:42:45.609Z  INFO 163 --- [ionShutdownHook] j.LocalContainerEntityManagerFactoryBean : Closing JPA EntityManagerFactory for persistence unit 'default'
2023-05-15T09:42:45.834Z  WARN 163 --- [ionShutdownHook] o.s.b.f.support.DisposableBeanAdapter    : Invocation of destroy method failed on bean with name 'inMemoryDatabaseShutdownExecutor': org.h2.jdbc.JdbcSQLNonTransientConnectionException: Database is already closed (to disable automatic closing at VM shutdown, add ";DB_CLOSE_ON_EXIT=FALSE" to the db URL) [90121-214]
2023-05-15T09:42:45.836Z  INFO 163 --- [ionShutdownHook] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown initiated...
2023-05-15T09:42:45.839Z  INFO 163 --- [ionShutdownHook] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Shutdown completed.
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  05:01 min
[INFO] Finished at: 2023-05-15T09:42:46Z
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.springframework.boot:spring-boot-maven-plugin:3.0.4:run (default-cli) on project spring-petclinic: Process terminated with exit code: 143 -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoExecutionException
```

* [x] Rename your docker as "petclinic-app"

<!---->

* [Official doc](https://docs.docker.com/engine/reference/commandline/rename/)

```
[INPUT]
docker tag petclinic:version1.0.dev petclinic-app:version1.0.dev
docker images

[OUTPUT]
REPOSITORY      TAG              IMAGE ID       CREATED          SIZE
petclinic-app   version1.0.dev   b6d10fb42b60   54 minutes ago   602MB
petclinic       dev              b6d10fb42b60   54 minutes ago   602MB
petclinic       int              b6d10fb42b60   54 minutes ago   602MB
petclinic       prod             b6d10fb42b60   54 minutes ago   602MB
petclinic       version1.0.dev   b6d10fb42b60   54 minutes ago   602MB
```

* [x] Restart your docker using the new name

```
[INPUT]
docker run --publish 8080:8080 petclinic-app:version1.0.dev

[OUTPUT]
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 24 source files to /app/target/classes
[INFO]
[INFO] --- maven-resources-plugin:3.3.0:testResources (default-testResources) @ spring-petclinic ---
[INFO] skip non existing resourceDirectory /app/src/test/resources
[INFO]
[INFO] --- maven-compiler-plugin:3.10.1:testCompile (default-testCompile) @ spring-petclinic ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 11 source files to /app/target/test-classes
[INFO] /app/src/test/java/org/springframework/samples/petclinic/vet/VetTests.java: /app/src/test/java/org/springframework/samples/petclinic/vet/VetTests.java uses or overrides a deprecated API.
[INFO] /app/src/test/java/org/springframework/samples/petclinic/vet/VetTests.java: Recompile with -Xlint:deprecation for details.
[INFO]
[INFO] <<< spring-boot-maven-plugin:3.0.4:run (default-cli) < test-compile @ spring-petclinic <<<
[INFO]
[INFO]
[INFO] --- spring-boot-maven-plugin:3.0.4:run (default-cli) @ spring-petclinic ---
[INFO] Attaching agents: []


              |\      _,,,--,,_
             /,`.-'`'   ._  \-;;,_
  _______ __|,4-  ) )_   .;.(__`'-'__     ___ __    _ ___ _______
 |       | '---''(_/._)-'(_\_)   |   |   |   |  |  | |   |       |
 |    _  |    ___|_     _|       |   |   |   |   |_| |   |       | __ _ _
 |   |_| |   |___  |   | |       |   |   |   |       |   |       | \ \ \ \
 |    ___|    ___| |   | |      _|   |___|   |  _    |   |      _|  \ \ \ \
 |   |   |   |___  |   | |     |_|       |   | | |   |   |     |_    ) ) ) )
 |___|   |_______| |___| |_______|_______|___|_|  |__|___|_______|  / / / /
 ==================================================================/_/_/_/

:: Built with Spring Boot :: 3.0.4


2023-05-15T09:55:25.936Z  INFO 162 --- [  restartedMain] o.s.s.petclinic.PetClinicApplication     : Starting PetClinicApplication using Java 17.0.7 with PID 162 (/app/target/classes started by root in /app)
2023-05-15T09:55:25.938Z  INFO 162 --- [  restartedMain] o.s.s.petclinic.PetClinicApplication     : No active profile set, falling back to 1 default profile: "default"
2023-05-15T09:55:25.964Z  INFO 162 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : Devtools property defaults active! Set 'spring.devtools.add-properties' to 'false' to disable
2023-05-15T09:55:25.964Z  INFO 162 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : For additional web related logging consider setting the 'logging.level.web' property to 'DEBUG'
2023-05-15T09:55:26.372Z  INFO 162 --- [  restartedMain] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data JPA repositories in DEFAULT mode.
2023-05-15T09:55:26.399Z  INFO 162 --- [  restartedMain] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 23 ms. Found 2 JPA repository interfaces.
2023-05-15T09:55:26.667Z  INFO 162 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2023-05-15T09:55:26.673Z  INFO 162 --- [  restartedMain] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2023-05-15T09:55:26.673Z  INFO 162 --- [  restartedMain] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.5]
2023-05-15T09:55:26.705Z  INFO 162 --- [  restartedMain] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2023-05-15T09:55:26.706Z  INFO 162 --- [  restartedMain] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 740 ms
2023-05-15T09:55:26.753Z  INFO 162 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2023-05-15T09:55:26.840Z  INFO 162 --- [  restartedMain] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Added connection conn0: url=jdbc:h2:mem:ea0801f9-2b07-4ed7-bb65-d6adb0e5ea24 user=SA
2023-05-15T09:55:26.841Z  INFO 162 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2023-05-15T09:55:26.846Z  INFO 162 --- [  restartedMain] o.s.b.a.h2.H2ConsoleAutoConfiguration    : H2 console available at '/h2-console'. Database available at 'jdbc:h2:mem:ea0801f9-2b07-4ed7-bb65-d6adb0e5ea24'
2023-05-15T09:55:26.940Z  INFO 162 --- [  restartedMain] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [name: default]
2023-05-15T09:55:26.964Z  INFO 162 --- [  restartedMain] org.hibernate.Version                    : HHH000412: Hibernate ORM core version 6.1.7.Final
2023-05-15T09:55:27.119Z  INFO 162 --- [  restartedMain] SQL dialect                              : HHH000400: Using dialect: org.hibernate.dialect.H2Dialect
2023-05-15T09:55:27.511Z  INFO 162 --- [  restartedMain] o.h.e.t.j.p.i.JtaPlatformInitiator       : HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2023-05-15T09:55:27.516Z  INFO 162 --- [  restartedMain] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2023-05-15T09:55:27.956Z  INFO 162 --- [  restartedMain] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2023-05-15T09:55:27.959Z  INFO 162 --- [  restartedMain] o.s.b.a.e.web.EndpointLinksResolver      : Exposing 13 endpoint(s) beneath base path '/actuator'
2023-05-15T09:55:28.000Z  INFO 162 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2023-05-15T09:55:28.009Z  INFO 162 --- [  restartedMain] o.s.s.petclinic.PetClinicApplication     : Started PetClinicApplication in 2.215 seconds (process running for 2.407)
```

* [ ] Display all running dockers with this output format

<!---->

* [Official doc](https://docs.docker.com/config/formatting/)

Result expected:

```
IMAGE                              PORTS.                  NAMES
eclipse-petclinic:version1.0.dev   0.0.0.0:80->8080/tcp.   petclinic-server
```

```
[INPUT]
docker ps --format "table {{.Image}}\t{{.Ports}}\t{{.Names}}"

[OUTPUT]
IMAGE                          PORTS                    NAMES
petclinic-app:version1.0.dev   0.0.0.0:8080->8080/tcp   recursing_liskov
```

