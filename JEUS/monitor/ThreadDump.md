## ThreadDump

특정 Java Process의 동작상태 파악 목적.

### Jstack 분석 (JDK 1.6 이상에서 가능)

ex) Server1에 deploy된 프로세스

jstack [PID] > [아무이름].txt
jstack 921 > server1dum.txt

![image](https://user-images.githubusercontent.com/38831314/146486798-ae4e2958-6407-49f1-b1fb-14b8ea03a315.png)


