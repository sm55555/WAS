## ThreadDump

특정 Java Process의 동작상태 파악 목적.

### Jstack 분석 (JDK 1.6 이상에서 가능)

ex) Server1에 deploy된 프로세스

jstack [PID] > [아무이름].txt
jstack 921 > server1dum.txt

![image](https://user-images.githubusercontent.com/38831314/146486798-ae4e2958-6407-49f1-b1fb-14b8ea03a315.png)


- 장애 발생시 Thread Dump생성할 때는, 일정한 간격을 두고 2~3차례 생성하도록 한다.
- 시간간격은 시스템 상황을 고려하여 5~20 second의 범위에 한정한다.
- Thread Dump 생성시 HeapDump 동시 생성 옵션이 설정되어 있다면  JVM Hang이 발생한다.
- Thread Dump가 생성되는 동안 JVM Lock이 발생하여, Service가 순간순간 멈추는 현상이 발생함을 명심한다.



