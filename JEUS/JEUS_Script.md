## 기본 명령어

#### 비밀번호 webadmin 노출 기동

```
vi dsboot
startDomainAdminServer -domain jeus_domain -u administrator -p jeusadmin -cachelogin
```

![image](https://user-images.githubusercontent.com/38831314/143995873-f6900300-b2dd-4a70-a145-22fe9ed33cd7.png)

.jeuspasswd를 /home/jeus8/jeus8/bin/jeusEncode 로 복사하고 사용 해야한다 !

#### 비밀번호 암호화 webadmin 기동

```
startDomainAdminServer -domain jeus_domain -u administrator -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode  -cachelogin
```

#### 비밀번호 암호화 webadmin 종료

```
vi dsdown
jeusadmin -host `hostname`:9736 -domain jeus_domain -u administrator -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin local-shutdown
```


```
vi dsa
jeusadmin -host `hostname`:10000 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin
```

#### 노드매니저 기동

안된다면 logs 폴더를 만들어 주자 ! 

![image](https://user-images.githubusercontent.com/38831314/143997070-cc2dbf58-5c91-41a2-b80c-275626d05b6d.png)


```
vi nmboot
LOGDATE=`date "+%y%m%d%H%M%S"`
nohup startNodeManager > /home/jeus8/jeus8/logs/nodemanager/nm_$LOGDATE.log &
```

#### 노드매니저 종료

```
vi nmdown
stopNodeManager -properties /home/jeus8/jeus8/nodemanager/jeusnm.xml
```

```
vi msboot
startManagedServer -dasurl `hostname`:9736 -domain jeus_domain -server server1  -u administrator -cachelogin -f /home/jeus8/jeus8/bin/jeusEncode
```


![image](https://user-images.githubusercontent.com/38831314/143998169-4825a306-7653-45c1-9978-bfe56db36189.png)


```
vi msdown
jeusadmin -host `hostname`:10010 -domain jeus_domain -u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode -cachelogin "local-shutdown -to 120"
```


### JVM 옵션

```
-Xms512m -Xmx512m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m
-verbose:gc
-XX:+PrintGCDetails -XX:+PrintGCTimeStamps -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC
-Xloggc:/home/jeus8/jeus8/logs/gclog/server2_gc.log
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/home/jeus8/jeus8/logs/dump/
```


### application 디플로이

```
mkdir /home/jeus8/webapps
```

```
cp /home/jeus8/install/edutest.zip /home/jeus8/webapps
jar -xvf /home/jeus8/webapps/edutest.zip
```
