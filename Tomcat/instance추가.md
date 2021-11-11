## 인스턴스 추가

#### Case 1. nginx + tomcat

(1) /etc/nginx/conf.d/virtual.conf

```
upstream abc {
        ip_hash;
        server 127.0.0.1:8080;

}

upstream abc-test {
        ip_hash;
        server 127.0.0.1:8081;

}

server {
    listen 80;
    #listen [::]:80;
    server_name  abc.co.kr;
    #if ($http_x_forwarded_proto = 'http'){
    #return 301 https://$host$request_uri;
    #}
    access_log   /var/log/nginx/access_abc.log;
    error_log    /var/log/nginx/error_abc.log;
    # 클라이언트가 업로드 할 수 있는 파일 크기 한도
    client_max_body_size 100M;
    proxy_set_header X-Real-IP $remote_addr;
    # 이를 통해 해당 헤더의 첫번째 값으로 요청을 보낸 클라이언트의 IP 주소를 알 수 있음
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;

        location /
        {
                return 301 https://$host$request_uri;
                proxy_pass http://abc;
                limit_except GET POST { deny all; }
                autoindex off;
        }
}

server {
    listen 80;
    #listen [::]:80;
    server_name  abc-test.co.kr;
    #if ($http_x_forwarded_proto = 'http'){
    #return 301 https://$host$request_uri;
    #}
    access_log   /var/log/nginx/access_abc-test.log;
    error_log    /var/log/nginx/error_abc-test.log;
    # 클라이언트가 업로드 할 수 있는 파일 크기 한도
    client_max_body_size 100M;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;

        location /
        {
                #return 301 https://$host$request_uri;
                proxy_pass http://abc-test;
                limit_except GET POST { deny all; }
                autoindex off;
        }
}
```

(2) 새로운 apache 폴더 구성 및 Server.xml 포트 변경

cp -rp로 복사한다. war파일 오래 걸릴 수 있어 주의

```

기존 설정

<Server port="8005" shutdown="SHUTDOWN">
...
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
...
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />

신규 설정

<Server port="8105" shutdown="SHUTDOWN">
...
<Connector port="8081" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8543" />
               
...
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />

```

(3) startup, shutdown sh 관리
(4) DB 연동 IP 설정(tomcat내 DB 설정 있으면)

