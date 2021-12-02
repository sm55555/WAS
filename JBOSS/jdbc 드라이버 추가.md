1. JDBC module 설정
 - maria DB
 modules 경로 : /data/was/jboss/jboss-eap-7.2/modules.ext/com

 1) maria/main 디렉토리 생성
   mkdir -p maria/main 

 2) jdbc module 복사
   cp /home/appadmin/mariadb-java-client-2.7.3.jar  /data/was/jboss/jboss-eap-7.2/modules.ext/com/maria/main/

 3) module.xml 파일 생성
   경로 :  /data/was/jboss/jboss-eap-7.2/modules.ext/com/maira/main
 * 수정사항 : module name, resource-root path
   vim module.xml
 ------
<?xml version="1.0" encoding="UTF-8"?>

<module name="com.maria" xmlns="urn:jboss:module:1.8">  --> module name 변경
    <resources>
        <resource-root path="mariadb-java-client-2.7.3.jar"/>   --> jdbc jar 명 입력
    </resources>
    <dependencies>
        <module name="javax.api"/>
        <module name="javax.transaction.api"/>
    </dependencies>
</module>
 ------

2. datasource 설정
1. standalone.xml의 datasource, driver 설정 변경 및 추가 
  경로 : /data/was/domains/hgdev-was1/configuration/standalone.xml
-----------
                    <connection-url>jdbc:mariadb:aurora://hghan-dev.cluster-c4iyx6guogte.ap-northeast-2.rds.amazonaws.com:3831/hanway_dev_gw?autoReconnect=true</connection-url>
...
                  <driver>maria</driver>
...
                    <driver name="maria" module="com.maria">
                        <driver-class>org.mariadb.jdbc.Driver</driver-class>
                    </driver> 
