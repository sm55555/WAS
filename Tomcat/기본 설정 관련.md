# Tomcat 기본 설정 관련

되도록 기동 시키는 유저는 따로 만들자.

만약 A 라는 유저로 기동하다가 Root로 변경하면 권한에 대한 문제 발생.

[조치 방법]

server.xml에 checkedOsUsers="root" 추가하면된다.

```
<Server port="8005" shutdown="SHUTDOWN">
  ...
  ...
  ...
  <Listener className="org.apache.catalina.security.SecurityListener" checkedOsUsers="root"/>
```

# Tomcat version 확인

bin 폴더에서 ./version.sh 실행

![image](https://user-images.githubusercontent.com/38831314/121829424-7401cf80-ccfd-11eb-8fe7-1c4e9767dbff.png)


# catalina.sh VS setenv.sh

bin 폴더에 위치한다.

![image](https://user-images.githubusercontent.com/38831314/121829865-ac55dd80-ccfe-11eb-8275-4dc0c3cde16c.png)

catalina.sh는 자바 옵션 설정 및 톰캣 로그 경로등 각종 설정을 할 수 있다.

setenv.sh는 톰캣 구동 시 실행 환경 설정 파일이다.

톰캣 시작 -> startup.sh 호출 -> catalina.sh 호출 -> setenv.sh (파일이 존재하는 경우 설정을 반영한다.)



