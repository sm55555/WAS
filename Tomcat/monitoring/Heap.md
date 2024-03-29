# 톰캣 Heap 분석

### 실시간 PID 모니터링

1초에 한번 씩 출력 3000회 반복
```
jstat -gcutil [PID] 1000 3000
```

ps -ef | grep tomcat 후 해당 PID 검색한다.

```
sudo jmap -heap [PID]
```

![image](https://user-images.githubusercontent.com/38831314/115180210-0c217500-a110-11eb-8ac6-007ade598ec1.png)


만약 Old Generation의 사용량이 지속적으로 증가한다면 memory leak을 의심해봐야 한다.
New Generation, Old Generation으 비율은 기본 1:2이다


### 메모리 힙덤프 추출

```
jmap dump:format=b,file=<output filename> <pid>
```

예시

```
[root@test ~]$ jmap -dump:format=b,file=heap.hprof29991
Dumping heap to /home/temp//heap.hprof ...
Heap dump file created
[root@test ~]$
```

생성된 hprof 파일 Eclipse Meomory Analyzer.md를 참고해 분석


### 참고 URL 네이버 D2

https://d2.naver.com/helloworld/37111

https://d2.naver.com/helloworld/1329

https://d2.naver.com/helloworld/1326256
