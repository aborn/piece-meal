# 老的class仍然存在
今天上线一个java web,我发现，我之前的写的一个bean仍然被初始化了。什么情况？
赶紧打开war包里的class文件看下

```
ls target/classes/*
➜  pelpa-web git:(master) ls target/pelpa/WEB-INF/classes/org/popkit/leap/monitor
BuildingExcutorPool$1.class  BuildingTask.class  entity                      FetcherExcutorPool.class  RoundStatusMonitor.class  RoundSupervisor.class
BuildingExcutorPool.class    EachActor.class     FetcherExcutorPool$1.class  FetcherTask.class         RoundSupervisor$1.class   utils
```

果然有个.class文件仍然存在。
## key words
部署,java web,mvn

## 原因
因为部署前没有进行mvn clean,我之前的部署脚本是这样写的：
```shell
mvn compile
mvn package -Dmaven.test.skip=ture
${CATALINA_HOME}/bin/catalina.sh start
```

## 解决
修改后的部署脚本为：
```
mvn clean;
mvn install;
mvn compile
mvn package -Dmaven.test.skip=ture
${CATALINA_HOME}/bin/catalina.sh start
```

## 参考
https://github.com/popkit/pelpa/blob/master/scripts/deploy.sh
