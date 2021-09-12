## Original src from [apache/flink-docker](https://github.com/apache/flink-docker)  and [version 1.13.2](https://github.com/apache/flink-docker/tree/master/1.13/scala_2.12-java11-debian)

* To update new-est dockerfile for new release `apache flink`  access this repo [apache/flink-docker](https://github.com/apache/flink-docker) then choose your verison

* If arm64 type host machine, Just change the base image of `Dockerfile`  from  ` openjdk:11-jre` for x64 ---> `arm64v8/openjdk:11-jre-buster` to support arm64 build


* change `maybe_enable_jemalloc` function from `docker-entrypint.sh` to use `jemalloc` on `arm64` cpu :
```sh
maybe_enable_jemalloc() {
    if [ "${DISABLE_JEMALLOC:-false}" == "false" ]; then
        
        if [ "$(uname -m)" == "aarch64" ]; then
            echo "load libjemalloc for arm64v8 arch "
            export LD_PRELOAD=$LD_PRELOAD:/usr/lib/aarch64-linux-gnu/libjemalloc.so
        else
            echo "load libjemalloc for x86/64 arch "
            export LD_PRELOAD=$LD_PRELOAD:/usr/lib/x86_64-linux-gnu/libjemalloc.so
        fi   
    fi
}
```

* To Build image :   `docker-compose  -f ./docker-compose-build.yml build` 





* To start java flink cluster :  `docker-compose  -f ./docker-compose.yml up -d` 
    * 1 x  jobmanager
    * 2 x  taskmanager ( taskmanager1 and taskmanager2)
    * each taskmanager have 2 slot ==> total slot = 2taskmanager x 2slot = 4 slot
    * vist http://your_flink_ip:8081/ to view the cluster status and deploy you new job

* Reference link
    * [flink docker setup](https://ci.apache.org/projects/flink/flink-docs-master/docs/deployment/resource-providers/standalone/docker/)








