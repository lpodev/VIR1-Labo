# Step 1 - Run the project outside Docker

- [Official Source](https://docs.docker.com/language/java/build-images/)

## Get the project source code

- Clone the repo

```bash
git clone https://github.com/spring-projects/spring-petclinic.git
```

<<<<<<< HEAD
- Read carefully the readme file

<!---->

- [x] What type of application is it ? Application Web
- [x] Which database engine is used ? MySQL or PostgreSQL
- [x] Do we need to install the package manager _MAVEN_ before building the project ? No, it's optional, you can choose between Maven or Gradle.
=======
* Read the readme file carefully

<!---->

* [ ] What type of application is it?
* [ ] Which database engine is used?
* [ ] Do we need to install the package manager _MAVEN_ before building the project?
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8

<!---->

- Inspect the dependencies (pom.xml)

<!---->

<<<<<<< HEAD
- [x] Which version of Java should compatible with the code provided ? Java 17 or newer
=======
* [ ] Which version of Java should be compatible with the code provided?
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8

## Setup Java components

### Check your current Java installation

<<<<<<< HEAD
- [x] Where is java installed ?
=======
* [ ] Where is Java installed?
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8

```
[INPUT]
which java

[OUTPUT]
/usr/bin/java
```

<<<<<<< HEAD
- [x] Which current compiler is installed (JDK) ?
=======
* [ ] Which current compiler is installed (JDK)?

<pre><code><strong>[INPUT]
</strong>//TODO

[OUTPUT]
//TODO
</code></pre>

* [ ] Which current runtime is installed (JRE)?
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8

```
[INPUT]
java --version

[OUTPUT]
openjdk 20.0.1 2023-04-18
OpenJDK Runtime Environment (build 20.0.1+9-29)
OpenJDK 64-Bit Server VM (build 20.0.1+9-29, mixed mode, sharing)
```

<<<<<<< HEAD
- [x] Which current runtime is installed (JRE) ?

```
[INPUT]
java --version

[OUTPUT]
openjdk 20.0.1 2023-04-18
OpenJDK Runtime Environment (build 20.0.1+9-29)
OpenJDK 64-Bit Server VM (build 20.0.1+9-29, mixed mode, sharing)
```

- [x] Do we need to install the java virtual machine (JVM) ?

```
No, JDK already contains JVM so we can run our java program
=======
* [ ] Do we need to install the Java virtual machine (JVM)?

```
//TODO
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8
```

### Install the Open JDK

<<<<<<< HEAD
- [Oracle Download Web Site](https://jdk.java.net/20/)

- Accept the end user license before trying
- Then get the target url (cookies.

```bash
=======
* [Oracle Download WebSite](https://jdk.java.net/20/)

{% hint style="info" %}
* Accept the end user license before trying, then
* Then get the target URL (cookies).
{% endhint %}

```powershell
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8
[INPUT]
curl https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1_macos-aarch64_bin.tar.gz --output openjdk.tar.gz

[OUTPUT]
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  183M  100  183M    0     0  3470k      0  0:00:53  0:00:53 --:--:-- 4360k
```

#### Check the archive integrity before installing the JDK

- [Get the hash provided by Oracle](https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1_macos-aarch64_bin.tar.gz.sha256)
- Generate your local hash based on the archive downloaded ([help](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.3))
- Compare both hashes...

<<<<<<< HEAD
```bash
=======
```powershell
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8
[INPUT]
shasum -a 256 openjdk.tar.gz

[OUTPUT]
78ae5bb4c96632df8d3f776919c95653d1afd3e715981c4d33be5b3c81d05420  openjdk.tar.gz
```

#### Unzip jdk archive

```bash
[INPUT]
tar -xf openjdk.tar.gz

[OUTPUT]
No output
```

#### Move the unzip folder to Programs Folder

<<<<<<< HEAD
```bash
=======
```
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8
[INPUT]
sudo mv jdk-20.0.1.jdk /Library/Java/JavaVirtualMachines

[OUTPUT]
No output
```

#### Set environment variables

- [Java official documentation](https://dev.java/learn/getting-started/)

<!---->

- [x] Set JAVA\_HOME variable

```bash
[INPUT]
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-20.0.1.jdk
echo $JAVA_HOME

[OUTPUT]
/Library/Java/JavaVirtualMachines/jdk-20.0.1.jdk
```

- [x] Update PATH environment variable

<<<<<<< HEAD
Backup your current path before updating it.
`echo %PATH% > path.back`
=======
{% hint style="info" %}
Back up your current path before updating it.
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8

```bash
[INPUT]
echo $PATH > path.back

[OUTPUT]
<<<<<<< HEAD
No output
```

- [ ] Check the variables settings
=======
//TODO

```

* [ ] Check the variables
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8

```bash
[INPUT]
export PATH=$JAVA_HOME/bin:$PATH
which java

[OUTPUT]
<<<<<<< HEAD
/usr/bin/java
=======
//TODO

>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8
```

## Build and test the project

```bash
[INPUT]
mvn package

[OUTPUT]
[INFO]
[INFO] Results:
[INFO]
[WARNING] Tests run: 41, Failures: 0, Errors: 0, Skipped: 1
[INFO]
[INFO]
[INFO] --- jacoco:0.8.8:report (report) @ spring-petclinic ---
[INFO] Loading execution data file /Users/lpodev/dev/temp/spring-petclinic/target/jacoco.exec
[INFO] Analyzed bundle 'petclinic' with 21 classes
[INFO]
[INFO] --- jar:3.3.0:jar (default-jar) @ spring-petclinic ---
[INFO] Building jar: /Users/lpodev/dev/temp/spring-petclinic/target/spring-petclinic-3.0.0-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot:3.0.4:repackage (repackage) @ spring-petclinic ---
[INFO] Replacing main artifact with repackaged archive
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  18.228 s
[INFO] Finished at: 2023-05-08T11:54:52+02:00
[INFO] ------------------------------------------------------------------------
```

<<<<<<< HEAD
### Result expected

```bash
[INPUT]
./mvnw spring-boot:run

[OUTPUT]
[INFO] Scanning for projects...
[INFO]
[INFO] ------------< org.springframework.samples:spring-petclinic >------------
[INFO] Building petclinic 3.0.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] >>> spring-boot-maven-plugin:3.0.4:run (default-cli) > test-compile @ spring-petclinic >>>
[INFO]
[INFO] --- spring-javaformat-maven-plugin:0.0.38:validate (default) @ spring-petclinic ---
[INFO]
[INFO] --- maven-enforcer-plugin:3.1.0:enforce (enforce-java) @ spring-petclinic ---
[INFO]
[INFO] --- maven-checkstyle-plugin:3.2.1:check (nohttp-checkstyle-validation) @ spring-petclinic ---
[INFO] You have 0 Checkstyle violations.
[INFO]
[INFO] --- jacoco-maven-plugin:0.8.8:prepare-agent (default) @ spring-petclinic ---
[INFO] argLine set to -javaagent:/Users/lpodev/.m2/repository/org/jacoco/org.jacoco.agent/0.8.8/org.jacoco.agent-0.8.8-runtime.jar=destfile=/Users/lpodev/dev/temp/spring-petclinic/target/jacoco.exec
[INFO]
[INFO] --- git-commit-id-maven-plugin:5.0.0:revision (default) @ spring-petclinic ---
[INFO] dotGitDirectory /Users/lpodev/dev/temp/spring-petclinic/.git
[INFO] Collected git.build.user.name with value LPOdev
[INFO] Collected git.build.user.email with value lpodevco@gmail.com
[INFO] Collected git.branch with value main
[INFO] --always = true
[INFO] --dirty = -dirty
[INFO] --abbrev = 7
[INFO] Tag refs [[Ref[refs/tags/1.5.x=c36452a2c34443ae26b4ecbba4f149906af14717(-1)]]]
[INFO] Created map: [{}]
[INFO] evalCommit is [c73419abb74d16d6568e02983dba56a2c888c7c8]
[INFO] Collected git.commit.id.describe with value c73419a
[INFO] Collected git.commit.id.describe-short with value c73419a
[INFO] Collected git.commit.id with value c73419abb74d16d6568e02983dba56a2c888c7c8
[INFO] Collected git.commit.id.abbrev with value c73419a
[INFO] Collected git.dirty with value false
[INFO] Collected git.commit.user.name with value jcw1031
[INFO] Collected git.commit.user.email with value jcw001031@gmail.com
[INFO] Collected git.commit.message.full with value Owener class's addVisit() method return type change to void
[INFO] Collected git.commit.message.short with value Owener class's addVisit() method return type change to void
[INFO] Collected git.commit.time with value 2023-04-26T14:42:30+0200
[INFO] Collected git.commit.author.time with value 2023-04-22T11:52:55+0200
[INFO] Collected git.commit.committer.time with value 2023-04-22T11:52:55+0200
[INFO] Collected git.remote.origin.url with value https://github.com/spring-projects/spring-petclinic.git
[INFO] Collected git.tags with value
[INFO] evalCommit is [c73419abb74d16d6568e02983dba56a2c888c7c8]
[INFO] Tag refs [[Ref[refs/tags/1.5.x=c36452a2c34443ae26b4ecbba4f149906af14717(-1)]]]
[INFO] Created map: [{}]
[INFO] Collected git.closest.tag.name with value
[INFO] evalCommit is [c73419abb74d16d6568e02983dba56a2c888c7c8]
[INFO] Tag refs [[Ref[refs/tags/1.5.x=c36452a2c34443ae26b4ecbba4f149906af14717(-1)]]]
[INFO] Created map: [{}]
[INFO] Collected git.closest.tag.commit.count with value
[INFO] Collected git.total.commit.count with value 849
[INFO] Collected git.local.branch.ahead with value 0
[INFO] Collected git.local.branch.behind with value 0
[INFO] Collected git.build.time with value 2023-05-08T11:55:58+0200
[INFO] Collected git.build.version with value 3.0.0-SNAPSHOT
[INFO] Collected git.build.host with value MacBook-Air-de-Luis.local
[INFO] including property git.tags in results
[INFO] including property git.build.version in results
[INFO] including property git.branch in results
[INFO] including property git.build.host in results
[INFO] including property git.commit.id in results
[INFO] including property git.commit.user.email in results
[INFO] including property git.local.branch.behind in results
[INFO] including property git.commit.author.time in results
[INFO] including property git.build.user.name in results
[INFO] including property git.dirty in results
[INFO] including property git.closest.tag.commit.count in results
[INFO] including property git.commit.user.name in results
[INFO] including property git.commit.id.abbrev in results
[INFO] including property git.commit.id.describe-short in results
[INFO] including property git.total.commit.count in results
[INFO] including property git.commit.id.describe in results
[INFO] including property git.build.user.email in results
[INFO] including property git.commit.message.short in results
[INFO] including property git.commit.committer.time in results
[INFO] including property git.closest.tag.name in results
[INFO] including property git.local.branch.ahead in results
[INFO] including property git.commit.time in results
[INFO] including property git.build.time in results
[INFO] including property git.commit.message.full in results
[INFO] including property git.remote.origin.url in results
[INFO] Reading existing properties file [/Users/lpodev/dev/temp/spring-petclinic/target/classes/git.properties] (for module petclinic)...
[INFO] Properties file [/Users/lpodev/dev/temp/spring-petclinic/target/classes/git.properties] is up-to-date (for module petclinic)...
[INFO]
[INFO] --- spring-boot-maven-plugin:3.0.4:build-info (default) @ spring-petclinic ---
[INFO]
[INFO] --- maven-resources-plugin:3.3.0:resources (default-resources) @ spring-petclinic ---
[INFO] Copying 3 resources
[INFO] Copying 43 resources
[INFO]
[INFO] --- maven-compiler-plugin:3.10.1:compile (default-compile) @ spring-petclinic ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-resources-plugin:3.3.0:testResources (default-testResources) @ spring-petclinic ---
[INFO] skip non existing resourceDirectory /Users/lpodev/dev/temp/spring-petclinic/src/test/resources
[INFO]
[INFO] --- maven-compiler-plugin:3.10.1:testCompile (default-testCompile) @ spring-petclinic ---
[INFO] Nothing to compile - all classes are up to date
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


2023-05-08T11:55:59.068+02:00  INFO 81142 --- [  restartedMain] o.s.s.petclinic.PetClinicApplication     : Starting PetClinicApplication using Java 20.0.1 with PID 81142 (/Users/lpodev/dev/temp/spring-petclinic/target/classes started by lpodev in /Users/lpodev/dev/temp/spring-petclinic)
2023-05-08T11:55:59.071+02:00  INFO 81142 --- [  restartedMain] o.s.s.petclinic.PetClinicApplication     : No active profile set, falling back to 1 default profile: "default"
2023-05-08T11:55:59.091+02:00  INFO 81142 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : Devtools property defaults active! Set 'spring.devtools.add-properties' to 'false' to disable
2023-05-08T11:55:59.091+02:00  INFO 81142 --- [  restartedMain] .e.DevToolsPropertyDefaultsPostProcessor : For additional web related logging consider setting the 'logging.level.web' property to 'DEBUG'
2023-05-08T11:55:59.474+02:00  INFO 81142 --- [  restartedMain] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data JPA repositories in DEFAULT mode.
2023-05-08T11:55:59.502+02:00  INFO 81142 --- [  restartedMain] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 24 ms. Found 2 JPA repository interfaces.
2023-05-08T11:55:59.770+02:00  INFO 81142 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2023-05-08T11:55:59.784+02:00  INFO 81142 --- [  restartedMain] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2023-05-08T11:55:59.784+02:00  INFO 81142 --- [  restartedMain] o.apache.catalina.core.StandardEngine    : Starting Servlet engine: [Apache Tomcat/10.1.5]
2023-05-08T11:55:59.820+02:00  INFO 81142 --- [  restartedMain] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2023-05-08T11:55:59.821+02:00  INFO 81142 --- [  restartedMain] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 729 ms
2023-05-08T11:55:59.867+02:00  INFO 81142 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2023-05-08T11:55:59.957+02:00  INFO 81142 --- [  restartedMain] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Added connection conn0: url=jdbc:h2:mem:f6195fb0-718f-47fd-8a60-402479385e39 user=SA
2023-05-08T11:55:59.958+02:00  INFO 81142 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Start completed.
2023-05-08T11:55:59.962+02:00  INFO 81142 --- [  restartedMain] o.s.b.a.h2.H2ConsoleAutoConfiguration    : H2 console available at '/h2-console'. Database available at 'jdbc:h2:mem:f6195fb0-718f-47fd-8a60-402479385e39'
2023-05-08T11:56:00.080+02:00  INFO 81142 --- [  restartedMain] o.hibernate.jpa.internal.util.LogHelper  : HHH000204: Processing PersistenceUnitInfo [name: default]
2023-05-08T11:56:00.107+02:00  INFO 81142 --- [  restartedMain] org.hibernate.Version                    : HHH000412: Hibernate ORM core version 6.1.7.Final
2023-05-08T11:56:00.239+02:00  INFO 81142 --- [  restartedMain] SQL dialect                              : HHH000400: Using dialect: org.hibernate.dialect.H2Dialect
2023-05-08T11:56:00.633+02:00  INFO 81142 --- [  restartedMain] o.h.e.t.j.p.i.JtaPlatformInitiator       : HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2023-05-08T11:56:00.637+02:00  INFO 81142 --- [  restartedMain] j.LocalContainerEntityManagerFactoryBean : Initialized JPA EntityManagerFactory for persistence unit 'default'
2023-05-08T11:56:01.125+02:00  INFO 81142 --- [  restartedMain] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2023-05-08T11:56:01.129+02:00  INFO 81142 --- [  restartedMain] o.s.b.a.e.web.EndpointLinksResolver      : Exposing 13 endpoint(s) beneath base path '/actuator'
2023-05-08T11:56:01.169+02:00  INFO 81142 --- [  restartedMain] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2023-05-08T11:56:01.179+02:00  INFO 81142 --- [  restartedMain] o.s.s.petclinic.PetClinicApplication     : Started PetClinicApplication in 2.26 seconds (process running for 2.435)
```
=======
### Result expected 

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
>>>>>>> 34def1ae84276ab970bd3f781ab863653599ceb8
