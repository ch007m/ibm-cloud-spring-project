# IBM Comparison

## Development & Build

### OpenLiberty and Spring Boot
  
- Info: https://jaxenter.com/ibm-liberty-update-146472.html
- Platforms: cloudfoundry, docker or baremetal: https://www.ibm.com/cloud/blog/open-liberty-loves-spring
- Format supported: jar/war or osgi bundles: http://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/4/897/ENUS218-354/index.html&request_locale=en
- Guides: https://openliberty.io/guides/

### Tooling


### Code generator

A Spring Boot project can be created using one of the following [approaches](https://developer.ibm.com/microservice-builder/2017/08/03/creating-new-java-microservice-microservice-builder/)
- Portal `IBM Cloud` from where you can select `Spring Boot`
- `ibmcloud dev` tool or
- [Liberty App Accelerator](http://liberty-app-accelerator.wasdev.developer.ibm.com/start/)

An example of the project generated using the IBM cloud is available [here](spring-project)

### Cloud Building

IBM proposes a dual docker build approach as described [hereafter](https://openliberty.io/blog/2018/07/02/creating-dual-layer-docker-images-for-spring-boot-apps.html)
The Spring project created at the previous step will be next build using [`Docker`](Dockerfile) and uploaded on the IBM cloud platform using a [helm chart](spring-project/chart)
The final image of the application will be created from the [ibm java docker image](https://hub.docker.com/_/ibmjava?tab=description) - `FROM ibmjava:8-sfj` which is a image created top
of [ubuntu](https://github.com/ibmruntimes/ci.docker/blob/a1994e0c3f71ef3ca4c25a5b8e57bb7bd5ec27ff/ibmjava/8/sfj/ubuntu/Dockerfile)

sfj is a **S**mall **F**ootprint **J**RE, available on Linux operating systems only, contains a lightweight version of the IBM® runtime environment for Java™.- https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.80.doc/user/small_jre.html
