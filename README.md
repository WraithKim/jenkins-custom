# Jenkins with Docker CLI

## Description

Jenkins image with Docker CLI and BlueOcean.  
This image is from jenkins tutorial. You can find here.  
<https://www.jenkins.io/doc/book/installing/docker/>  

However, this image doesn't use Docker-in-docker(a.k.a. dind).  
Instead, this uses host docker socket, so image built from jenkins will install in host docker.  
Check out this article for further reasons.  
<https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/>

Must run as root because docker socket need root permission.  
Alternatively, you can run without root when you manually change the ownership after docker container initialized.

## Build

``` sh
$ docker build --tag jenkins-custom .
```

## Usage

### Linux shell

``` sh
$ docker run --detach \
-v "$(pwd)/jenkins-data:/var/jenkins_home" \
-v /var/run/docker.sock:/var/run/docker.sock \
-p 8080:8080 \
--name jenkins-docker \
-u root \
wraithkim/jenkins-custom
```

### Windows powershell

``` powershell
PS> docker run --detach `
-v "$(pwd)/jenkins-data:/var/jenkins_home" `
-v /var/run/docker.sock:/var/run/docker.sock `
-p 8080:8080 `
--name jenkins-docker `
-u root `
wraithkim/jenkins-custom
```
