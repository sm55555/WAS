### Jeus Monitor

case : CPU 과점유 상태

#### 1. 서버에서 Full GC 시간대를 확인 너무 자주일어나면 프로그램 문제 (개발자 연락 or 프로세스 리부팅)

grep -i "full gc" test_gc.log

![image](https://user-images.githubusercontent.com/38831314/141706121-a1a0d59a-df53-40a3-b79b-d296c957697b.png)

#### 2. Monitoring -> Thread 새로 고침 후 계속 쌓이는거 확인 -> 발견되면 서버 로그 확인

![image](https://user-images.githubusercontent.com/38831314/141706749-3188e4a0-684b-4984-ae4d-53141e4759ca.png)

#### 3. Monitoring -> Web -> bacukup 수 확인 계속 증가하면 불법 봇으로 인한 유입 가능성 존재

![image](https://user-images.githubusercontent.com/38831314/141706811-11d1b5ee-8ca6-46d1-b20a-a8df6b846268.png)

#### 4. Monitoring -> Connection Pool Active 수 확인 Max만큼 계속 올라가면 문제

Min, Max 맞추는게 좋다 최대한 Connection Pool 많이 잡아도 서버에 큰 영향은 없다. 하지만 Connection Pool이 생기므로 적당히 분배해야 함

![image](https://user-images.githubusercontent.com/38831314/141707183-ed75efe7-a489-4a0f-8c08-fd43a9837a5b.png)









