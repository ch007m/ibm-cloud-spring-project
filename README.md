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

## Cloud Development

See doc available on the IBM cloud web site - https://cloud.ibm.com/docs/cli?topic=cloud-cli-developing

The procedure to install the tool is [defined here](https://cloud.ibm.com/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli) and will require to install or have the [following tools](https://github.com/IBM-Cloud/ibm-cloud-developer-tools/blob/master/linux-installer/idt-installer).

- Homebrew (Mac only)
- Git
- Docker
- Helm
- kubectl
- curl
- IBM Cloud Developer Tools plug-in
- IBM Cloud Functions plug-in
- IBM Cloud Container Registry plug-in
- IBM Cloud Kubernetes Service plug-in
- sdk-gen plug-in 

**Remark**: The interactive mode of the tool don't offer the possibility to select the version of Spring Boot like also the starters

If the tool has been installed like the plugin `dev`

```bash
/Users/dabou/MyApplications/ibmtools/ibmcloud install dev
``` 

then execute this command to create an application

```bash
/Users/dabou/MyApplications/ibmtools/ibmcloud dev create
Log in to IBM Cloud using the ./ibmcloud/ibmcloud login command to synchronize your apps with the IBM Cloud dashboard, and to enable the use of IBM Cloud services in your app.
Do you wish to continue without logging in?
?  [Y/n]> Y

============================================================================================================================================================================================================================
Select an application type:

 1. Blank App
 2. Backend Service / Web App
 3. Mobile App
-----------------------------------------------------------------------
 0. Exit

============================================================================================================================================================================================================================
? Enter selection number:> 2

============================================================================================================================================================================================================================
Select a language:

 1. Go
 2. Java - MicroProfile / Java EE
 3. Java - Spring
 4. Node
 5. Python - Django
 6. Python - Flask
 7. Scala
 8. Swift
-----------------------------------------------------------------------
 0. Return to the previous selection

============================================================================================================================================================================================================================
? Enter selection number:> 3

============================================================================================================================================================================================================================
Select a Starter Kit:

APPSERVICE
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 1. Java BFF Example with Spring - A starter building backend-for-frontend APIs in Java, using the Spring framework.

 2. Java Microservice with Spring - A starter building a microservice backend in Java, using the Spring framework.

 3. Java Web App with Spring - A starter that provides a basic web serving application in Java, using the Spring framework.

-----------------------------------------------------------------------
 0. Return to the previous selection

============================================================================================================================================================================================================================
? Enter selection number:> 2

? Enter a name for your application> demo1


The app, demo1, has been successfully saved into the current directory.
```

Now that the application has been created locally, we will build and deploy it on the IBM Cloud platform using one of the hosting environment supported

As a Docker container on a Kubernetes cluster
As a Cloud Foundry app
As a serverless function
As VMware
As a virtual machine
On high-performance Bare Metal Servers

As the existing account is free of charge, we will use the cloudfoundry hosting environment to install it 

```bash
ibmcloud login -u chm56 -p TqGSe_4dLq\!xcN\! -r eu-gb
ibmcloud target --cf 
Targeted Cloud Foundry (https://api.eu-gb.bluemix.net)
Targeted org chm56
Select a space (or press enter to skip):
1. dev
2. snowdrop
Enter a number> 2
Targeted space snowdrop

                      
API endpoint:      https://cloud.ibm.com   
Region:            eu-gb   
User:              cmoulliard@redhat.com   
Account:           Charles Moulliard's Account (83a4b90035934171a66e48152d22d912)   
Resource group:    Default   
CF API endpoint:   https://api.eu-gb.bluemix.net (API version: 2.128.0)   
Org:               chm56   
Space:             snowdrop   

ibmcloud dev get-credentials

```

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

IBM Cloud Tool: 

Plugins: https://plugins.cloud.ibm.com/ui/repository.html

## Social

[IBM Slack server](https://ibm-cloud-tech.slack.com)
[#spring-at-ibm](https://ibm-cloud-tech.slack.com/?redir=%2Fmessages%2FC85E8V4G1)