vi dsboot
startDomainAdminServer -domain jeus_domain -u administrator -p jeusadmin -cachelogin

-u wasadmin -f /home/jeus8/jeus8/bin/jeusEncode  -cachelogin

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
