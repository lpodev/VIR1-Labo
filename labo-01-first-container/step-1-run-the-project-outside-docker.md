# Step 1 - Run the project outside Docker

* [Official Source](https://docs.docker.com/language/java/build-images/)

## Get the project source code

* Clone the repo

```
git clone https://github.com/spring-projects/spring-petclinic.git
```

* Read carefully the readme file

<!---->

* [x] What type of application is it ? Application Web
* [x] Which database engine is used ? MySQL or PostgreSQL
* [x] Do we need to install the package manager _MAVEN_ before building the project ? No, it's optional, you can choose between Maven or Gradle.

<!---->

* Inspect the dependencies (pom.xml)

<!---->

* [x] Which version of Java should compatible with the code provided ? Java 17 or newer

## Setup Java components

### Check your current java installation

* [x] Where is java installed ?

```
[INPUT]
which java

[OUTPUT]
/usr/bin/java
```

* [x] Which current compiler is installed (JDK) ?

```
[INPUT]
java --version

[OUTPUT]
openjdk 20.0.1 2023-04-18
OpenJDK Runtime Environment (build 20.0.1+9-29)
OpenJDK 64-Bit Server VM (build 20.0.1+9-29, mixed mode, sharing)
```

* [x] Which current runtime is installed (JRE) ?

```
[INPUT]
java --version

[OUTPUT]
openjdk 20.0.1 2023-04-18
OpenJDK Runtime Environment (build 20.0.1+9-29)
OpenJDK 64-Bit Server VM (build 20.0.1+9-29, mixed mode, sharing)
```

* [x] Do we need to install the java virtual machine (JVM) ?

```
No, JDK already contains JVM so we can run our java program
```

### Install the Open JDK

* [Oracle Download Web Site](https://jdk.java.net/20/)

{% hint style="info" %}
* Accept the end user license before trying
* Then get the target url (cookies.
{% endhint %}

```
[INPUT]
curl https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1_macos-aarch64_bin.tar.gz --output openjdk.tar.gz

[OUTPUT]
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  183M  100  183M    0     0  3470k      0  0:00:53  0:00:53 --:--:-- 4360k
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Powershell output during sdk download process</p></figcaption></figure>

#### Check the archive integrity before installing the JDK

* [Get the hash provided by Oracle](https://download.java.net/java/GA/jdk20.0.1/b4887098932d415489976708ad6d1a4b/9/GPL/openjdk-20.0.1\_windows-x64\_bin.zip.sha256)
* Generate your local hash based on the archive downloaded ([help](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-filehash?view=powershell-7.3))
* Compare both hashes...

```
[INPUT]
shasum -a 256 openjdk.tar.gz

[OUTPUT]
78ae5bb4c96632df8d3f776919c95653d1afd3e715981c4d33be5b3c81d05420  openjdk.tar.gz
```

#### Unzip jdk archive

```
[INPUT]
tar -xf openjdk.tar.gz

[OUTPUT]
No output
```

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Powershell output during unzip process</p></figcaption></figure>

#### Move the unzip folder to Programs Folder

```
[INPUT]
sudo mv jdk-20.0.1.jdk /Library/Java/JavaVirtualMachines

[OUTPUT]
No output
```

#### Set environment variables

* [Java official documentation](https://dev.java/learn/getting-started/)

<!---->

* [ ] Set JAVA\_HOME variable

```
[INPUT]
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-20.0.1.jdk
echo $JAVA_HOME

[OUTPUT]
/Library/Java/JavaVirtualMachines/jdk-20.0.1.jdk
```

* [ ] Update PATH environment variable

{% hint style="info" %}
Backup your current path before updating it.

echo %PATH% > path.back
{% endhint %}

```
[INPUT]
export PATH=$JAVA_HOME/bin:$PATH
which java

[OUTPUT]
/usr/bin/java
```

* [ ] Check the variables settings

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```

## Build and test the project

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```


### Result expected

```
[INPUT]
//TODO

[OUTPUT]
//TODO
```
