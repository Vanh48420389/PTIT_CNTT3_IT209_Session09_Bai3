# Báo Cáo Thực Hành Bài 3: Đóng Gói Trang Web HTML Tĩnh Vào Docker Image

## 1. Build Docker Image (my-html-app:v1)
```bash
$ docker build -t my-html-app:v1 .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 104B 0.0s done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/nginx:alpine
#2 DONE 0.0s

#3 [internal] load .dockerignore
#3 transferring context: 2B 0.0s done
#3 DONE 0.0s

#4 [internal] load build context
#4 transferring context: 71B 0.0s done
#4 DONE 0.0s

#5 [1/2] FROM docker.io/library/nginx:alpine@sha256:df221db836e1754089190208cee7eeda94f233197056426eda74a43ab1abeac2
#5 resolve docker.io/library/nginx:alpine@sha256:df221db836e1754089190208cee7eeda94f233197056426eda74a43ab1abeac2 0.0s done
#5 DONE 0.0s

#6 [2/2] COPY index.html /usr/share/nginx/html/index.html
#6 CACHED

#7 exporting to image
#7 exporting layers done
#7 exporting manifest sha256:f2d4133404fdf08fea83e2f12defcd816d8d2780164e42ecca2cad4ac0c0eb9b done
#7 exporting config sha256:9c6aa43628665a9404a49d34cc6a563fa363d4f6f7f580eb3f3667b9c39aafe0 done
#7 exporting attestation manifest sha256:81f49b50b1ec53418c168d3b82e3672dccc6a3dadf801003701e5cb97c3de68d 0.0s done
#7 exporting manifest list sha256:1608dcf1b6d95b2e268ac992ebc049d751070faefaf42cf57881efec5002250f 0.0s done
#7 naming to docker.io/library/my-html-app:v1 done
#7 unpacking to docker.io/library/my-html-app:v1 done
#7 DONE 0.1s
```

## 2. Khởi chạy Container (cổng 8081:80)
```bash
$ docker run -d -p 8081:80 --name html-app my-html-app:v1
ff0f44b352ca4783f333c70343d8a5adc93020c980641d43a92ee343fb31324d
```

## 3. Kiểm tra trạng thái Container (docker ps)
```bash
$ docker ps
CONTAINER ID   IMAGE            COMMAND                  CREATED                  STATUS                  PORTS                                     NAMES
ff0f44b352ca   my-html-app:v1   "/docker-entrypoint.…"   Less than a second ago   Up Less than a second   0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   html-app
3b1eeb0e7528   nginx:alpine     "/docker-entrypoint.…"   10 minutes ago           Up 10 minutes           0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web
```

## 4. Kiểm tra phản hồi Web Server (curl http://localhost:8081)
```bash
$ curl -i http://localhost:8081
  % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
  0      0   0      0   0      0      0      0                              0100     34 100     34   0      0    163      0                              0100     34 100     34   0      0    121      0                              0100     34 100     34   0      0     95      0                              0
HTTP/1.1 200 OK
Server: nginx/1.31.6
Date: Sun, 11 Oct 2026 16:29:41 GMT
Content-Type: text/html
Content-Length: 34
Last-Modified: Sun, 11 Oct 2026 16:25:31 GMT
Connection: keep-alive
ETag: "6acbb87b-22"
Accept-Ranges: bytes

<h1>Hello Docker Session 09!</h1>
```

## 5. Dọn dẹp Container
```bash
$ docker stop html-app && docker rm html-app
html-app
html-app
```
