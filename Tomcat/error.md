#### webapps 파일 문제

apache2/apache-tomcat-8.0.45/webapps/TEST 해당 파일 확인

```
Caused by: java.lang.IllegalArgumentException: The main resource set specified [/apache2/apache-tomcat-8.0.45/webapps/TEST] is not valid
        at org.apache.catalina.webresources.StandardRoot.createMainResourceSet(StandardRoot.java:731)
        at org.apache.catalina.webresources.StandardRoot.startInternal(StandardRoot.java:689)
        at org.apache.catalina.util.LifecycleBase.start(LifecycleBase.java:145)
```

#### 기동은 되는데 안올라올 때

apache2/apache-tomcat-8.0.45/webapps 하위 권한 톰캣 기동이랑 일치해야한다.
