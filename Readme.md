## Original src from [apache/flink-docker](https://github.com/apache/flink-docker)  and [version 1.13.2](https://github.com/apache/flink-docker/tree/master/1.13/scala_2.12-java11-debian)

* To update new-est dockerfile for new release `apache flink`  access this repo [apache/flink-docker](https://github.com/apache/flink-docker) then choose your verison

* If arm64 type host machine, Just change the base image of `Dockerfile`  from  ` openjdk:11-jre` for x64 ---> `arm64v8/openjdk:11-jre-buster` to support arm64 build
* To Build image :   `docker-compose  -f ./docker-compose-build.yml build` 





