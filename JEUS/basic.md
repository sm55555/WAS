### 제우스 기본 상식

DB 클러스터링도 메모리 잡아먹음

administratorServer(DAS의 한가지 기능) 켜야 -> NodeManager 기동해야 -> 하위 MS들을 관리할 수 있다.

```
ps -ef | grep java 시 adminServer, NodeManager 확인 가능
```

MS는 콘솔내 or 서버에서 관리 가능하지만, administratorServer, NodeManager는 콘솔내에서만 관리 가능하다


