# IBM Comparison

## OpenLiberty and Spring Boot
  
OpenLiberty is a JavaEE platform designed as an OSGI runtime and where we can deploy Spring Boot applications packaged as jar, war files.
The platform supports Spring Boot 1.5.x or 2.x  and a [few starters](https://www.ibm.com/support/knowledgecenter/en/SSD28V_9.0.0/com.ibm.websphere.wlp.core.doc/ae/rwlp_springboot.html):

spring-boot-starter
spring-boot-starter-web
spring-boot-starter-websocket
spring-boot-starter-webflux

OpenLiberty supports 3 [different platforms](https://www.ibm.com/cloud/blog/open-liberty-loves-spring) : cloudfoundry, docker/kubernetes or baremetal

References:

- Guides: https://openliberty.io/guides/
- Format supported: jar/war or osgi bundles: http://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/4/897/ENUS218-354/index.html&request_locale=en


## Code generator

A Spring Boot project can be created using one of the following [approaches](https://developer.ibm.com/microservice-builder/2017/08/03/creating-new-java-microservice-microservice-builder/)
- Portal `IBM Cloud` from where you can select `Spring Boot`
- `ibmcloud dev` tool or
- [Liberty App Accelerator](http://liberty-app-accelerator.wasdev.developer.ibm.com/start/)

An example of the project generated using the IBM cloud is available [here](spring-project)

## Cloud Building

IBM proposes a dual docker build approach as described [hereafter](https://openliberty.io/blog/2018/07/02/creating-dual-layer-docker-images-for-spring-boot-apps.html).

The Spring project created at the previous step will be next build using [`Docker`](Dockerfile) and uploaded on the IBM cloud platform using a [helm chart](spring-project/chart)
The final image of the application will be created from the [ibm java docker image](https://hub.docker.com/_/ibmjava?tab=description) - `FROM ibmjava:8-sfj` which is a image created top
of [ubuntu](https://github.com/ibmruntimes/ci.docker/blob/a1994e0c3f71ef3ca4c25a5b8e57bb7bd5ec27ff/ibmjava/8/sfj/ubuntu/Dockerfile)

## Docker images

IBM proposes different developers [Java 8](https://github.com/ibmruntimes/ci.docker/tree/a1994e0c3f71ef3ca4c25a5b8e57bb7bd5ec27ff/ibmjava) images supporting :
- Apache Maven: https://github.com/ibmruntimes/ci.docker/tree/a1994e0c3f71ef3ca4c25a5b8e57bb7bd5ec27ff/ibmjava/8
- [IBM SDK](https://developer.ibm.com/javasdk/downloads/sdk8/) (alpine, ubi, ubuntu): https://github.com/ibmruntimes/ci.docker/tree/a1994e0c3f71ef3ca4c25a5b8e57bb7bd5ec27ff/ibmjava/8/sdk
- JRE (rhel, ubuntu, alpine): https://github.com/ibmruntimes/ci.docker/tree/a1994e0c3f71ef3ca4c25a5b8e57bb7bd5ec27ff/ibmjava/8/jre
- SFJ (light JRE)

[sfj](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.80.doc/user/small_jre.html) is a **S**mall **F**ootprint **J**RE, available on Linux operating systems only, contains a lightweight version of the IBM® runtime environment for Java™.
The [IBM SDK](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.80.doc/user/java_sdk.html) is equivalent to OpenJDK as it provides the Java runtime plus also development [tools](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.80.doc/user/java_sdk.html)

## Tooling