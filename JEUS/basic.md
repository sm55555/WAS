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

### 로그 꿀팁

Cauesd by 를 검색하자...
