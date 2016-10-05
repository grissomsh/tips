# Jenkins 2.0 + CloudBees Docker Pipeline Plugin

Jenkins 2.0发布之后，一直想使用一下Pipeline，国庆闲来无事就试玩了一下。

## Install Jenkins 2.0
* 由于网络的原因，建议在国外云主机上安装，例如在在DigitalOcean上开一台主机（我选择了Centos 7.2）
* 安装[Docker Engine](https://docs.docker.com/engine/installation/linux/centos/)
* Download [official Jenkins Image](https://hub.docker.com/_/jenkins/)
* Run: ``docker run -d -p 8080:8080 -p 50000:50000 jenkins``

安装过程中会在日志中打印一个admin的密钥，如果是-d方式启动，可以用如下命令查看``docker logs jenkins``

## Install CloudBees Docker Pipeline plugin

* 菜单选择如下：``jenkins->系统管理->管理插件->可选插件``
* 查找CloudBees Docker Pipeline, 选择安装并重启Jenkins
* [使用说明](https://go.cloudbees.com/docs/cloudbees-documentation/cje-user-guide/chapter-docker-workflow.html), 在使用之前请先装一个支持Docker的Slave节点

[CloudBees](https://www.cloudbees.com)是不是有点眼熟？"[The DevOps 2.0 Toolkit: Automating the Continuous Deployment Pipeline with Containerized Microservices Kindle Edition](https://www.amazon.com/dp/B01BJ4V66M)"一书的作者Viktor Farcic就来自CloudBees。



## Add a slave node
* 安装Slave很简单，[参考](https://wiki.jenkins-ci.org/display/JENKINS/Step+by+step+guide+to+set+up+master+and+slave+machines)，其实自己摸索一下即可。
* Slave节点预先不需要安装任何东西
* Master访问Slave有几种方式，我使用了SSH User Name With Private Key
* 设置Key请[参考](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)
* 建议选择From the Jenkins master ~/.ssh

## First Docker Pipeline job

其中Pipeline script如下:

~~~
node('docker'){
    docker.image('maven:3.3.3-jdk-8').inside {
      git 'https://github.com/codecentric/spring-boot-admin.git'
      sh 'mvn -B clean'
    }
}
~~~

其中node是选择具有docker标签的节点（不然没有安装Docker就会失败）

结果如下：

~~~
Started by user grissom
[Pipeline] node
Running on jenkins-slave-01 in /root/jenkins/workspace/test
[Pipeline] {
[Pipeline] sh
[test] Running shell script
+ docker inspect -f . maven:3.3.3-jdk-8

Error: No such image, container or task: maven:3.3.3-jdk-8
[Pipeline] sh
[test] Running shell script
+ docker pull maven:3.3.3-jdk-8
3.3.3-jdk-8: Pulling from library/maven
5c90d4a2d1a8: Pulling fs layer
ab30c63719b1: Pulling fs layer
c6072700a242: Pulling fs layer
5f444d070427: Pulling fs layer
620b5227cf38: Pulling fs layer
3cfd33220efa: Pulling fs layer
864a98a84dd2: Pulling fs layer
734cc28150de: Pulling fs layer
9d837ce35c41: Pulling fs layer
5f444d070427: Waiting
620b5227cf38: Waiting
3cfd33220efa: Waiting
864a98a84dd2: Waiting
734cc28150de: Waiting
9d837ce35c41: Waiting
ab30c63719b1: Verifying Checksum
ab30c63719b1: Download complete
c6072700a242: Verifying Checksum
c6072700a242: Download complete
5c90d4a2d1a8: Verifying Checksum
5c90d4a2d1a8: Download complete
3cfd33220efa: Verifying Checksum
3cfd33220efa: Download complete
620b5227cf38: Verifying Checksum
620b5227cf38: Download complete
5f444d070427: Verifying Checksum
5f444d070427: Download complete
734cc28150de: Verifying Checksum
734cc28150de: Download complete
9d837ce35c41: Verifying Checksum
9d837ce35c41: Download complete
864a98a84dd2: Verifying Checksum
864a98a84dd2: Download complete
5c90d4a2d1a8: Pull complete
ab30c63719b1: Pull complete
c6072700a242: Pull complete
5f444d070427: Pull complete
620b5227cf38: Pull complete
3cfd33220efa: Pull complete
864a98a84dd2: Pull complete
734cc28150de: Pull complete
9d837ce35c41: Pull complete
Digest: sha256:518b1cc95440282f98881aaa4da85e0dd8eca419e4f1e62bd3b28eaf6ce52f9b
Status: Downloaded newer image for maven:3.3.3-jdk-8
[Pipeline] withDockerContainer
$ docker run -t -d -u 0:0 -w /root/jenkins/workspace/test -v /root/jenkins/workspace/test:/root/jenkins/workspace/test:rw -v /root/jenkins/workspace/test@tmp:/root/jenkins/workspace/test@tmp:rw -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** -e ******** --entrypoint cat maven:3.3.3-jdk-8
[Pipeline] {
[Pipeline] git
Cloning the remote Git repository
Cloning repository https://github.com/codecentric/spring-boot-admin.git
 > git init /root/jenkins/workspace/test # timeout=10
Fetching upstream changes from https://github.com/codecentric/spring-boot-admin.git
 > git --version # timeout=10
 > git fetch --tags --progress https://github.com/codecentric/spring-boot-admin.git +refs/heads/*:refs/remotes/origin/*
 > git config remote.origin.url https://github.com/codecentric/spring-boot-admin.git # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/codecentric/spring-boot-admin.git # timeout=10
Fetching upstream changes from https://github.com/codecentric/spring-boot-admin.git
 > git fetch --tags --progress https://github.com/codecentric/spring-boot-admin.git +refs/heads/*:refs/remotes/origin/*
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
 > git rev-parse refs/remotes/origin/origin/master^{commit} # timeout=10
Checking out Revision c1ff8c4b32a23ba2b9c407e02d6f987a1c8a4af1 (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f c1ff8c4b32a23ba2b9c407e02d6f987a1c8a4af1
 > git branch -a -v --no-abbrev # timeout=10
 > git checkout -b master c1ff8c4b32a23ba2b9c407e02d6f987a1c8a4af1
First time build. Skipping changelog.
[Pipeline] sh
[test] Running shell script
+ mvn -B clean
[INFO] Scanning for projects...
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-starter-parent/1.4.1.RELEASE/spring-boot-starter-parent-1.4.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-starter-parent/1.4.1.RELEASE/spring-boot-starter-parent-1.4.1.RELEASE.pom (8 KB at 4.1 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-dependencies/1.4.1.RELEASE/spring-boot-dependencies-1.4.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-dependencies/1.4.1.RELEASE/spring-boot-dependencies-1.4.1.RELEASE.pom (87 KB at 371.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/spring-framework-bom/4.3.3.RELEASE/spring-framework-bom-4.3.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/spring-framework-bom/4.3.3.RELEASE/spring-framework-bom-4.3.3.RELEASE.pom (5 KB at 65.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/data/spring-data-releasetrain/Hopper-SR3/spring-data-releasetrain-Hopper-SR3.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/data/spring-data-releasetrain/Hopper-SR3/spring-data-releasetrain-Hopper-SR3.pom (5 KB at 64.0 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/data/build/spring-data-build/1.8.3.RELEASE/spring-data-build-1.8.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/data/build/spring-data-build/1.8.3.RELEASE/spring-data-build-1.8.3.RELEASE.pom (6 KB at 50.3 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/integration/spring-integration-bom/4.3.2.RELEASE/spring-integration-bom-4.3.2.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/integration/spring-integration-bom/4.3.2.RELEASE/spring-integration-bom-4.3.2.RELEASE.pom (9 KB at 104.7 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/security/spring-security-bom/4.1.3.RELEASE/spring-security-bom-4.1.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/security/spring-security-bom/4.1.3.RELEASE/spring-security-bom-4.1.3.RELEASE.pom (5 KB at 71.9 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies/Camden.RELEASE/spring-cloud-dependencies-Camden.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies/Camden.RELEASE/spring-cloud-dependencies-Camden.RELEASE.pom (7 KB at 111.9 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.2.0.RELEASE/spring-cloud-dependencies-parent-1.2.0.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.2.0.RELEASE/spring-cloud-dependencies-parent-1.2.0.RELEASE.pom (7 KB at 84.0 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-commons-dependencies/1.1.3.RELEASE/spring-cloud-commons-dependencies-1.1.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-commons-dependencies/1.1.3.RELEASE/spring-cloud-commons-dependencies-1.1.3.RELEASE.pom (4 KB at 40.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.1.2.RELEASE/spring-cloud-dependencies-parent-1.1.2.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.1.2.RELEASE/spring-cloud-dependencies-parent-1.1.2.RELEASE.pom (7 KB at 77.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-netflix-dependencies/1.2.0.RELEASE/spring-cloud-netflix-dependencies-1.2.0.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-netflix-dependencies/1.2.0.RELEASE/spring-cloud-netflix-dependencies-1.2.0.RELEASE.pom (16 KB at 214.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.2.1.RELEASE/spring-cloud-dependencies-parent-1.2.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.2.1.RELEASE/spring-cloud-dependencies-parent-1.2.1.RELEASE.pom (7 KB at 92.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-stream-dependencies/Brooklyn.RELEASE/spring-cloud-stream-dependencies-Brooklyn.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-stream-dependencies/Brooklyn.RELEASE/spring-cloud-stream-dependencies-Brooklyn.RELEASE.pom (7 KB at 93.1 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-task-dependencies/1.0.3.RELEASE/spring-cloud-task-dependencies-1.0.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-task-dependencies/1.0.3.RELEASE/spring-cloud-task-dependencies-1.0.3.RELEASE.pom (3 KB at 29.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.1.1.RELEASE/spring-cloud-dependencies-parent-1.1.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-dependencies-parent/1.1.1.RELEASE/spring-cloud-dependencies-parent-1.1.1.RELEASE.pom (7 KB at 48.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-config-dependencies/1.2.0.RELEASE/spring-cloud-config-dependencies-1.2.0.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-config-dependencies/1.2.0.RELEASE/spring-cloud-config-dependencies-1.2.0.RELEASE.pom (4 KB at 47.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-consul-dependencies/1.1.0.RELEASE/spring-cloud-consul-dependencies-1.1.0.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-consul-dependencies/1.1.0.RELEASE/spring-cloud-consul-dependencies-1.1.0.RELEASE.pom (6 KB at 75.4 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-sleuth-dependencies/1.0.9.RELEASE/spring-cloud-sleuth-dependencies-1.0.9.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-sleuth-dependencies/1.0.9.RELEASE/spring-cloud-sleuth-dependencies-1.0.9.RELEASE.pom (5 KB at 63.1 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-zookeeper-dependencies/1.0.3.RELEASE/spring-cloud-zookeeper-dependencies-1.0.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-zookeeper-dependencies/1.0.3.RELEASE/spring-cloud-zookeeper-dependencies-1.0.3.RELEASE.pom (6 KB at 69.4 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-security-dependencies/1.1.3.RELEASE/spring-cloud-security-dependencies-1.1.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-security-dependencies/1.1.3.RELEASE/spring-cloud-security-dependencies-1.1.3.RELEASE.pom (3 KB at 12.4 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-cloudfoundry-dependencies/1.0.1.RELEASE/spring-cloud-cloudfoundry-dependencies-1.0.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-cloudfoundry-dependencies/1.0.1.RELEASE/spring-cloud-cloudfoundry-dependencies-1.0.1.RELEASE.pom (3 KB at 30.0 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-bus-dependencies/1.2.0.RELEASE/spring-cloud-bus-dependencies-1.2.0.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-bus-dependencies/1.2.0.RELEASE/spring-cloud-bus-dependencies-1.2.0.RELEASE.pom (3 KB at 34.0 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-contract-dependencies/1.0.0.RELEASE/spring-cloud-contract-dependencies-1.0.0.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-contract-dependencies/1.0.0.RELEASE/spring-cloud-contract-dependencies-1.0.0.RELEASE.pom (8 KB at 107.2 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-aws-dependencies/1.1.3.RELEASE/spring-cloud-aws-dependencies-1.1.3.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/cloud/spring-cloud-aws-dependencies/1.1.3.RELEASE/spring-cloud-aws-dependencies-1.1.3.RELEASE.pom (6 KB at 49.2 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/com/amazonaws/aws-java-sdk-bom/1.11.18/aws-java-sdk-bom-1.11.18.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/com/amazonaws/aws-java-sdk-bom/1.11.18/aws-java-sdk-bom-1.11.18.pom (15 KB at 238.7 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/com/amazonaws/aws-java-sdk-pom/1.11.18/aws-java-sdk-pom-1.11.18.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/com/amazonaws/aws-java-sdk-pom/1.11.18/aws-java-sdk-pom-1.11.18.pom (9 KB at 151.9 KB/sec)
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO] 
[INFO] Spring Boot Admin
[INFO] spring-boot-admin-starter-client
[INFO] spring-boot-admin-server
[INFO] spring-boot-admin-server-ui
[INFO] spring-boot-admin-server-ui-activiti
[INFO] spring-boot-admin-server-ui-hystrix
[INFO] Spring Boot Admin Samples
[INFO] spring-boot-admin-sample
[INFO] spring-boot-admin-sample-war
[INFO] spring-boot-admin-sample-eureka
[INFO] spring-boot-admin-sample-consul
[INFO] spring-boot-admin-sample-zookeeper
[INFO] spring-boot-admin-sample-hazelcast
[INFO] Spring Boot Admin Docs
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building Spring Boot Admin 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-source-plugin/2.4/maven-source-plugin-2.4.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-source-plugin/2.4/maven-source-plugin-2.4.pom (7 KB at 98.3 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/25/maven-plugins-25.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/25/maven-plugins-25.pom (10 KB at 129.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/24/maven-parent-24.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/24/maven-parent-24.pom (37 KB at 514.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/apache/14/apache-14.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/apache/14/apache-14.pom (15 KB at 217.3 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-source-plugin/2.4/maven-source-plugin-2.4.jar
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-source-plugin/2.4/maven-source-plugin-2.4.jar (31 KB at 323.0 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-javadoc-plugin/2.10.4/maven-javadoc-plugin-2.10.4.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-javadoc-plugin/2.10.4/maven-javadoc-plugin-2.10.4.pom (16 KB at 172.1 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/28/maven-plugins-28.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/28/maven-plugins-28.pom (12 KB at 77.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/27/maven-parent-27.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/27/maven-parent-27.pom (40 KB at 401.6 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/apache/17/apache-17.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/apache/17/apache-17.pom (16 KB at 131.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-javadoc-plugin/2.10.4/maven-javadoc-plugin-2.10.4.jar
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-javadoc-plugin/2.10.4/maven-javadoc-plugin-2.10.4.jar (406 KB at 1341.7 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.6.1/maven-clean-plugin-2.6.1.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.6.1/maven-clean-plugin-2.6.1.pom (5 KB at 75.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/26/maven-plugins-26.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/26/maven-plugins-26.pom (12 KB at 188.2 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/25/maven-parent-25.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/25/maven-parent-25.pom (37 KB at 580.4 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/apache/15/apache-15.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/apache/15/apache-15.pom (15 KB at 232.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.6.1/maven-clean-plugin-2.6.1.jar
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.6.1/maven-clean-plugin-2.6.1.jar (29 KB at 294.5 KB/sec)
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin ---
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.pom (2 KB at 19.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.2.1/maven-2.2.1.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven/2.2.1/maven-2.2.1.pom (22 KB at 347.4 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/11/maven-parent-11.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/11/maven-parent-11.pom (32 KB at 390.7 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/apache/5/apache-5.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/apache/5/apache-5.pom (5 KB at 48.2 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.7/maven-shared-utils-0.7.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.7/maven-shared-utils-0.7.pom (5 KB at 74.2 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/20/maven-shared-components-20.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-components/20/maven-shared-components-20.pom (5 KB at 90.7 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.pom (965 B at 18.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.jar
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.7/maven-shared-utils-0.7.jar
[INFO] Downloading: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.jar
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.1/plexus-utils-1.1.jar
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/maven-plugin-api/2.2.1/maven-plugin-api-2.2.1.jar (13 KB at 135.8 KB/sec)
[INFO] Downloaded: https://repo.maven.apache.org/maven2/com/google/code/findbugs/jsr305/2.0.1/jsr305-2.0.1.jar (32 KB at 118.3 KB/sec)
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/apache/maven/shared/maven-shared-utils/0.7/maven-shared-utils-0.7.jar (167 KB at 615.2 KB/sec)
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/codehaus/plexus/plexus-utils/1.1/plexus-utils-1.1.jar (165 KB at 421.0 KB/sec)
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-starter-client 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-starter-client ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-server 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-server ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-server-ui 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-server-ui ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-server-ui-activiti 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-server-ui-activiti ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-server-ui-hystrix 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-server-ui-hystrix ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building Spring Boot Admin Samples 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-samples ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-sample 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] Downloading: https://repo.maven.apache.org/maven2/pl/project13/maven/git-commit-id-plugin/2.2.1/git-commit-id-plugin-2.2.1.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/pl/project13/maven/git-commit-id-plugin/2.2.1/git-commit-id-plugin-2.2.1.pom (12 KB at 91.3 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/sonatype/oss/oss-parent/9/oss-parent-9.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/sonatype/oss/oss-parent/9/oss-parent-9.pom (7 KB at 66.8 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/pl/project13/maven/git-commit-id-plugin/2.2.1/git-commit-id-plugin-2.2.1.jar
[INFO] Downloaded: https://repo.maven.apache.org/maven2/pl/project13/maven/git-commit-id-plugin/2.2.1/git-commit-id-plugin-2.2.1.jar (79 KB at 1003.9 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-maven-plugin/1.4.1.RELEASE/spring-boot-maven-plugin-1.4.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-maven-plugin/1.4.1.RELEASE/spring-boot-maven-plugin-1.4.1.RELEASE.pom (7 KB at 66.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-tools/1.4.1.RELEASE/spring-boot-tools-1.4.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-tools/1.4.1.RELEASE/spring-boot-tools-1.4.1.RELEASE.pom (2 KB at 16.5 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-parent/1.4.1.RELEASE/spring-boot-parent-1.4.1.RELEASE.pom
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-parent/1.4.1.RELEASE/spring-boot-parent-1.4.1.RELEASE.pom (26 KB at 348.7 KB/sec)
[INFO] Downloading: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-maven-plugin/1.4.1.RELEASE/spring-boot-maven-plugin-1.4.1.RELEASE.jar
[INFO] Downloaded: https://repo.maven.apache.org/maven2/org/springframework/boot/spring-boot-maven-plugin/1.4.1.RELEASE/spring-boot-maven-plugin-1.4.1.RELEASE.jar (63 KB at 808.2 KB/sec)
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-sample ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-sample-war 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-sample-war ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-sample-eureka 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-sample-eureka ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-sample-consul 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-sample-consul ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-sample-zookeeper 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-sample-zookeeper ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-boot-admin-sample-hazelcast 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-sample-hazelcast ---
[INFO]                                                                         
[INFO] ------------------------------------------------------------------------
[INFO] Building Spring Boot Admin Docs 1.4.3-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.6.1:clean (default-clean) @ spring-boot-admin-docs ---
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO] 
[INFO] Spring Boot Admin .................................. SUCCESS [  3.973 s]
[INFO] spring-boot-admin-starter-client ................... SUCCESS [  0.004 s]
[INFO] spring-boot-admin-server ........................... SUCCESS [  0.008 s]
[INFO] spring-boot-admin-server-ui ........................ SUCCESS [  0.002 s]
[INFO] spring-boot-admin-server-ui-activiti ............... SUCCESS [  0.021 s]
[INFO] spring-boot-admin-server-ui-hystrix ................ SUCCESS [  0.007 s]
[INFO] Spring Boot Admin Samples .......................... SUCCESS [  0.001 s]
[INFO] spring-boot-admin-sample ........................... SUCCESS [  0.818 s]
[INFO] spring-boot-admin-sample-war ....................... SUCCESS [  0.002 s]
[INFO] spring-boot-admin-sample-eureka .................... SUCCESS [  0.024 s]
[INFO] spring-boot-admin-sample-consul .................... SUCCESS [  0.002 s]
[INFO] spring-boot-admin-sample-zookeeper ................. SUCCESS [  0.051 s]
[INFO] spring-boot-admin-sample-hazelcast ................. SUCCESS [  0.011 s]
[INFO] Spring Boot Admin Docs ............................. SUCCESS [  0.002 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 15.001 s
[INFO] Finished at: 2016-10-05T08:21:56+00:00
[INFO] Final Memory: 35M/104M
[INFO] ------------------------------------------------------------------------
[Pipeline] }
$ docker stop baf7b24e27f1e5259831947c25941d50c1e2b941ef6eae25b00d1bd7c7149269
$ docker rm -f baf7b24e27f1e5259831947c25941d50c1e2b941ef6eae25b00d1bd7c7149269
[Pipeline] // withDockerContainer
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
~~~
