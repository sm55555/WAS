## WAS 기동 시 드라이버 로딩실패

#### WAS 기동시 jdbc driver를 로딩 하지 못하는 현상

- WAS 기동시 jdbc 드라이버를 로딩 하지 못함
- Datasource lookup fail 발생


###### 1. WAS 기동시 jdbc driver를 로딩 하지 못하는 현상

-> standalone.xml 을 다음과 같이 수정 :
<xa-datasource-class> 태그 삭제 및 <driver> 태그 내 module 이름을 com.oracle로 변경

```

                <drivers>
                    <driver name="maria" module="com.maria">
                        <driver-class>org.mariadb.jdbc.Driver</driver-class>
                    </driver>
                    <driver name="oracle" <strong>module="com.oracle"</strong>>
                    </driver>
                </drivers>
```
