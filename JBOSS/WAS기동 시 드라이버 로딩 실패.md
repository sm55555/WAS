## WAS 기동 시 드라이버 로딩실패

#### WAS 기동시 jdbc driver를 로딩 하지 못하는 현상

- WAS 기동시 jdbc 드라이버를 로딩 하지 못함
- Datasource lookup fail 발생


##### 1. WAS 기동시 jdbc driver를 로딩 하지 못하는 현상

-> standalone.xml 을 다음과 같이 수정

<xa-datasource-class> 태그 삭제 및 <driver> 태그 내 module 이름을 <strong>com.oracle</strong>로 변경

```

                <drivers>
                    <driver name="maria" module="com.maria">
                        <driver-class>org.mariadb.jdbc.Driver</driver-class>
                    </driver>
                    <driver name="oracle" module="com.oracle">
                    </driver>
                </drivers>
```
  
-> /data/was/jboss/jboss-eap-7.2/modules.ext/com/oracle/main/module.xml 수정
  
<module> 태그 내에 name을 <strong>com.oracle</strong>로 변경 (standalone.xml 과 동일하게 설정)

```
<module xmlns="urn:jboss:module:1.1" name="com.oracle">
    <resources>
        <resource-root path="ojdbc6.jar"/>
    </resources>
    <dependencies>
        <module name="javax.api"/>
        <module name="javax.transaction.api"/>
    </dependencies>
</module>
```

/data/was/jboss/jboss-eap-7.2/modules.ext/com/oracle/main에서 -> jdbc driver 파일의 권한을 jboss 계정으로 변경
-rw-r----- 1 jboss appgrp 3389454 Dec 29 14:52 ojdbc6.jar

  
2. Datasource lookup fail
-> jndi name 수정(standalone.xml)  
  
```
<datasource jndi-name="java:jboss/ORGABDS" pool-name="ORGABDS" enabled="true" use-java-context="true">
<connection-url>jdbc:oracle:thin:@hjgma-db03.cx6o7aubfgep.ap-northeast-2.rds.amazonaws.com:1521:hjgma03</connection-url>  
```  
  
Datasource connection test : bin 디렉토리 jboss-cli.sh 실행
  
```
[standalone@10.10.10.11:7877 /] /subsystem=datasources/data-source=ORGABDS:test-connection-in-pool
{
    "outcome" => "success",
    "result" => [true]
}
```
  
  
  
 
