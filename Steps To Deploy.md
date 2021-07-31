
# Deploy in Cloud Foundry

The SDK App creation by Bluemix doesnot contain manifest.yml and .cfignore files.

<br/>

> **manifest.yml**:
> 
> &nbsp;&nbsp;Contains the information for cf push, such as app name, memory, buildpack, host, and others.
> 
> &nbsp;&nbsp;This file must exist at application root level.

<br/>

> **.cfignore**:
> 
> &nbsp;&nbsp;Contains the list of file(s) to be ignored by Cloud Foundry.
> 
> &nbsp;&nbsp;This file works the same way as *.gitignore* and is optional.

<br/>

## Create a manifest file as: 
```yml
---  
applications:
- instances: 1
  timeout: 180
  name: <appname>
  buildpack: java_buildpack
  path: <jar filename with path relative to manifest.yml>
  disk_quota: <total_disk_size>
  memory: <application_memory_size>
  domain: <hosting_domain>
  host: <host_name>
  env:
    <ENV_KEY>: '<ENV-VALUE>'
```
<br/>

#### Example:
```yml
---
applications:
- instances: 1
  timeout: 180
  name: testjavaapp1
  buildpack: java_buildpack
  path: ./target/javaspringapp-1.0-SNAPSHOT.jar
  disk_quota: 1G
  memory: 512MB
  domain: mybluemix.net
  host: testjavaapp1
  env:
    JAVA_OPTS: '-XX:ReservedCodeCacheSize=32M -XX:MaxDirectMemorySize=32M'
    JBP_CONFIG_OPEN_JDK_JRE: '[memory_calculator: {stack_threads: 30}]'
```

<br/>

> ***mvn package***
> 
> This maven command will build application snapshot or artifactId (as mentioned in *pom.xml*, here it is *javaspringapp-1.0-SNAPSHOT.jar*).
> 
> It will also run end-point test

<br/>

> Once the build is succesfully finished, it's ready to be pushed/deployed:<br/>
> ***cf push \<appname\>***

<br/>

> If the app is successfully deployed, app-details will be displayed:<br/>
> 
> **requested state**: started<br/>
> **instances**: 1/1<br/>
> **usage**: 512M x 1 instances<br/>
> **urls**: \<url where the app is hosted\><br/>
> **last uploaded**: \<timestamp\><br/>
> **stack**: \<OS layer\><br/>
> **buildpack**: java_buildpack<br/>

<br>

### Happy Coding !
