
## 用yum安装JDK

### 1. 查看yum库中都有哪些jdk版本(暂时只发现了openjdk)
```
[root@localhost ~]# yum search java|grep jdk
ldapjdk-javadoc.x86_64 : Javadoc for ldapjdk
java-1.6.0-openjdk.x86_64 : OpenJDK Runtime Environment
java-1.6.0-openjdk-demo.x86_64 : OpenJDK Demos
java-1.6.0-openjdk-devel.x86_64 : OpenJDK Development Environment
java-1.6.0-openjdk-javadoc.x86_64 : OpenJDK API Documentation
java-1.6.0-openjdk-src.x86_64 : OpenJDK Source Bundle
java-1.7.0-openjdk.x86_64 : OpenJDK Runtime Environment
java-1.7.0-openjdk-demo.x86_64 : OpenJDK Demos
java-1.7.0-openjdk-devel.x86_64 : OpenJDK Development Environment
java-1.7.0-openjdk-javadoc.noarch : OpenJDK API Documentation
java-1.7.0-openjdk-src.x86_64 : OpenJDK Source Bundle
java-1.8.0-openjdk.x86_64 : OpenJDK Runtime Environment
java-1.8.0-openjdk-demo.x86_64 : OpenJDK Demos
java-1.8.0-openjdk-devel.x86_64 : OpenJDK Development Environment
java-1.8.0-openjdk-headless.x86_64 : OpenJDK Runtime Environment
java-1.8.0-openjdk-javadoc.noarch : OpenJDK API Documentation
java-1.8.0-openjdk-src.x86_64 : OpenJDK Source Bundle
ldapjdk.x86_64 : The Mozilla LDAP Java SDK
```
### 2. 选择版本,进行安装

//选择1.7版本进行安装
[root@localhost ~]# yum install java-1.7.0-openjdk
//安装完之后，默认的安装目录是在: /usr/lib/jvm/java-1.7.0-openjdk-1.7.0.75.x86_64

### 3.设置环境变量

[root@localhost ~]# vi /etc/profile

* 在profile文件中添加如下内容
```
#set java environment
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.181-3.b13.el7_5.x86_64
JRE_HOME=$JAVA_HOME/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```
* 让修改生效

[root@localhost java]# source /etc/profile
```
mkdir /opt/tomcat

wget http://www-us.apache.org/dist/tomcat/tomcat-8/v8.0.53/bin/apache-tomcat-8.0.53.tar.gz

cd /usr/local/tomcat
tar -zxvf apache-tomcat-8.0.53.tar.gz
mv /opt/tomcat/apache-tomcat-8.0.53.tar.gz /usr/local/tomcat/


vi /etc/systemd/system/tomcat.service
----------------------------------------------
[Unit]
Description=Tomcat
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=oneshot
ExecStart=/usr/local/tomcat/apache-tomcat-8.0.53/bin/startup.sh
ExecStop=/usr/local/tomcat/apache-tomcat-8.0.53/bin/shutdown.sh
ExecReload=/bin/kill -s HUP $MAINPID
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
------------------------------------------------

systemctl start tomcat.service    启动tomcat

systemctl stop tomcat.service     关闭tomcat

systemctl restart tomcat.service    重启tomcat
```
