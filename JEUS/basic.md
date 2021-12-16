### JEUS 기본 상식

DB 클러스터링도 메모리 잡아먹음 -> 세션 맺을 때 사용? 나중에 확인하기

administratorServer(DAS의 한가지 기능) 켜야 -> NodeManager 기동해야 -> 하위 MS들을 관리할 수 있다.

```
ps -ef | grep java 시 adminServer, NodeManager 확인 가능
```

![image](https://user-images.githubusercontent.com/38831314/143993770-c9ea185b-bd6f-446c-b166-69732afaa5e2.png)


MS start, stop은 콘솔 내 or 서버에서 관리 가능하지만, administratorServer, NodeManager는 서버내에서만 컨트롤 가능하다.

### webadmin 접속 방법

```
http://ip주소:[administratorServer Base Port]/webadmin
```

### 전체 로그 설정 방법

Domain에 설정한다. 물룬 서버마다 설정가능함. 서버 설정 값이 우선순위가 더 높다.

![image](https://user-images.githubusercontent.com/38831314/144006623-7b3a41b6-801e-4296-87fa-45bb54c59c81.png)

### 에러 로그 발견 꿀팁

Cauesd by 를 검색하자...


## 명령어들..

vi dsboot
startDomainAdminServer -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode  -cachelogin

vi dsdown
jeusadmin -host `hostname`:10000 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin local-shutdown

vi dsa
jeusadmin -host `hostname`:10000 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin

vi nmboot
LOGDATE=`date "+%y%m%d%H%M%S"`
nohup startNodeManager > /home/jeus8/jeus8/logs/nodemanager/nm_$LOGDATE.log &

vi nmdown
stopNodeManager -properties /home/jeus8/jeus8/nodemanager/jeusnm.xml

vi msboot
startManagedServer -dasurl `hostname`:10000 -domain jeus_domain -server $1  -u wasadmin –cachelogin –f /home/jeus8/jeus8/bin/jeusEncode

vi msdown
jeusadmin -host `hostname`:10010 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin "local-shutdown -to 120"

---

**JVM 옵션

-Xms512m -Xmx512m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m
-verbose:gc
-XX:+PrintGCDetails -XX:+PrintGCTimeStamps -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC
-Xloggc:/home/jeus8/jeus8/logs/gclog/server2_gc.log
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/home/jeus8/jeus8/logs/dump/


**  application 디플로이
mkdir /home/jeus8/webapps


cp /home/jeus8/install/edutest.zip /home/jeus8/webapps
jar -xvf /home/jeus8/webapps/edutest.zip


vi dsboot
startDomainAdminServer -domain jeus_domain -u administrator -f /home/jeus8/jeus8/bin/jeusEncode  -cachelogin

vi dsdown
jeusadmin -host `hostname`:10000 -domain jeus_domain -u administrator -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin local-shutdown

vi dsa
jeusadmin -host `hostname`:10000 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin

vi nmboot
LOGDATE=`date "+%y%m%d%H%M%S"`
nohup startNodeManager > /home/jeus8/jeus8/logs/nodemanager/nm_$LOGDATE.log &

vi nmdown
stopNodeManager -properties /home/jeus8/jeus8/nodemanager/jeusnm.xml

vi msboot
startManagedServer -dasurl `hostname`:10000 -domain jeus_domain -server $1  -u wasadmin –cachelogin –f /home/jeus8/jeus8/bin/jeusEncode

vi msdown
jeusadmin -host `hostname`:10010 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin "local-shutdown -to 120"

---

**JVM 옵션

-Xms512m -Xmx512m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m
-verbose:gc
-XX:+PrintGCDetails -XX:+PrintGCTimeStamps -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC
-Xloggc:/home/jeus8/jeus8/logs/gclog/server2_gc.log
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/home/jeus8/jeus8/logs/dump/


**  application 디플로이
mkdir /home/jeus8/webapps


cp /home/jeus8/install/edutest.zip /home/jeus8/webapps
jar -xvf /home/jeus8/webapps/edutest.zip
