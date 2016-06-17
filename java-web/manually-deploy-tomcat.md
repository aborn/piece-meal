在开发过程中，我们经常采用ide进行java项目的开发和自动部署。但在服务器上，我们不得不通过手工的方式进行部署我们的应用。通过以下几步完成手动部署tomcat应用：

## 下载tomcat
首先下载[Tomcat 7](https://tomcat.apache.org/download-70.cgi)，下载后将其解压到某个目录下：
```shell
➜  apache-tomcat-7.0.54 pwd
/home/popkit/software/apache-tomcat-7.0.54
➜  apache-tomcat-7.0.54 ls
bin  conf  lib  LICENSE  logs  NOTICE  RELEASE-NOTES  RUNNING.txt  temp  webapps  work
➜  apache-tomcat-7.0.54
```

## 设置环境变量
下载解压后，我们要设置两个环境变量（在.zshrc或者.bashrc里添加以下两行）：***CATALINA_HOME***和***CATALINA_BASE***，我这里将他们设置成一样的：
```shell
export CATALINA_HOME=/home/popkit/software/apache-tomcat-7.0.54
export CATALINA_BASE=$CATALINA_HOME
```

## 基本配置
修改$CATALINA_HOME/conf/server.xml，找到host对应的那项，修改为如下：
```xml
<Host name="localhost"  appBase="webapps"
	      unpackWARs="false" autoDeploy="false" deployXML="false"
	                xmlValidation="false" xmlNamespaceAware="false">
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log." suffix=".txt"
               pattern="%h %l %u %t "%r" %s %b" />
</Host>
```
注意上面几个参数（参数说明可以参考[官网的doc](https://tomcat.apache.org/tomcat-7.0-doc/config/host.html)）：  
1. appBase 是应用的根目录，可设置为绝对目录，也可设置为相对目录。这里的相对目录是相对于**$CATALINA_HOME**的，如果没有设置默认的appBase值为webapps。  
2.  unpackWARs 如果你想将appBase目录下的war包文件解压成可查看的目录格式，将这个值设置为true。注意：在appBase外的war包不会被解压。  
3. autoDeploy 当tomcat运行过程中，这个值设置用来是否定期地去检查新的应用或更新应用。如果设置为*true*，tomcat会定期地去检查appBase和xmlBase目录，并部署新的应用。同时，当xml描述文件修改时也会触发tomcat重新reload应用。默认值为*true*。最好，这里将其设置为*false*，因为你希望手动部署它。  
4. xmlBase 基于这个host的xml配置的根目录，这个目录包含了要部署该host的XML描述文件。可设置为绝对目录，也可设置为相对目录（相对目录是相对于**$CATALINA_BASE**）。如果没有设置，默认目录为：*conf/<engine_name>/<host_name>*，如下*conf/Catalina/localhost*  
```shell
➜  apache-tomcat-7.0.54 pwd
/home/popkit/software/apache-tomcat-7.0.54
➜  apache-tomcat-7.0.54 ls conf/Catalina/localhost
ROOT.xml
```
5. copyXML 如果你希望，在应用部署后，将应用中的context xml描述文件(/META-INF/context.xml)拷贝到xmlBase目录下，将这个参数设置为true。默认值为false。
6. deployXML 如果你不希望解析应用中的xml上下文描述文件(在应用的 /META-INF/context.xml)，将这个值设置为false。从安全的角度来考虑，你也应该将其设置为false。默认值为true。

## 打包部署
修改完成上面的server.xml后，在如下目录添加ROOT.xml
```
/home/popkit/software/apache-tomcat-7.0.54/conf/Catalina/localhost/
```
我的ROOT.xml文件内容如下：
```xml
<Context docBase="/home/popkit/pelpa/pelpa-web/target/pelpa" path="/" />
```
注意，我打的war包目录为*/home/popkit/pelpa/pelpa-web/target/pelpa*，根据自己的情况设置该值。可以通过mvn进行打包，注意打包前最好mvn clean下:
```shell
# clean first
mvn clean;
# package war
mvn package -Dmaven.test.skip=ture
```
