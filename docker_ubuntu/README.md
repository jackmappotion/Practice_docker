# docker install ubuntu


### 1. docker search ubuntu
```
❯ docker search ubuntu
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                           Ubuntu is a Debian-based Linux operating sys…   15992     [OK]
websphere-liberty                WebSphere Liberty multi-architecture images …   294       [OK]
open-liberty                     Open Liberty multi-architecture images based…   59        [OK]
neurodebian                      NeuroDebian provides neuroscience research s…   100       [OK]
ubuntu-debootstrap               DEPRECATED; use "ubuntu" instead                51        [OK]
ubuntu-upstart                   DEPRECATED, as is Upstart (find other proces…   114       [OK]
ubuntu/nginx                     Nginx, a high-performance reverse proxy & we…   91
ubuntu/cortex                    Cortex provides storage for Prometheus. Long…   3
ubuntu/squid                     Squid is a caching proxy for the Web. Long-t…   57
ubuntu/apache2                   Apache, a secure & extensible open-source HT…   58
ubuntu/mysql                     MySQL open source fast, stable, multi-thread…   48
ubuntu/kafka                     Apache Kafka, a distributed event streaming …   32
ubuntu/bind9                     BIND 9 is a very flexible, full-featured DNS…   52
ubuntu/redis                     Redis, an open source key-value store. Long-…   18
ubuntu/prometheus                Prometheus is a systems and service monitori…   41
ubuntu/postgres                  PostgreSQL is an open source object-relation…   27
ubuntu/zookeeper                 ZooKeeper maintains configuration informatio…   6
ubuntu/grafana                   Grafana, a feature rich metrics dashboard & …   9
ubuntu/memcached                 Memcached, in-memory keyvalue store for smal…   5
ubuntu/prometheus-alertmanager   Alertmanager handles client alerts from Prom…   8
ubuntu/dotnet-deps               Chiselled Ubuntu for self-contained .NET & A…   8
ubuntu/dotnet-runtime            Chiselled Ubuntu runtime image for .NET apps…   5
ubuntu/dotnet-aspnet             Chiselled Ubuntu runtime image for ASP.NET a…   6
ubuntu/cassandra                 Cassandra, an open source NoSQL distributed …   2
ubuntu/telegraf                  Telegraf collects, processes, aggregates & w…   4
```

### 2. docker pull ubuntu
> - docker pull ubuntu
> - docker pull ubuntu:latest
> - docker pull ubuntu:20.04

```
❯ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
79d0ea7dc1a8: Pull complete
Digest: sha256:dfd64a3b4296d8c9b62aa3309984f8620b98d87e47492599ee20739e8eb54fbf
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

### 3. docker images
```
❯ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    3f5ef9003cef   4 weeks ago   69.2MB
```


### 4. docker run -it --name my_ubuntu_container ubuntu
> - 명령어로 생성하기
>   - docker run -it --name my_ubuntu_container ubuntu
>       - docker run
>       - -i : interactive 표준입력 받는 옵션, 
>       - -t : 가상 터미널 환경 제공
>       - -name : 컨테이너 이름 지정
>       - ubuntu : 컨테이너를 실행할 이미지 지정하는것
> - Dockerfile로 생성하기
> - docker-compose로 생성하기

```
❯ docker run -it --name my_ubuntu_container ubuntu
root@90416d8418ee:/#
    -> 바로 들어가진다.
```
### 5. docker ps

```
❯ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### 6. docker start my_ubuntu_container
```
❯ docker start my_ubuntu_container
my_ubuntu_container
```

### 7. docker ps
```
❯ docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED              STATUS         PORTS     NAMES
90416d8418ee   ubuntu    "/bin/bash"   About a minute ago   Up 3 seconds             my_ubuntu_container
```

### 7. docker attach my_ubuntu_container
```
❯ docker attach my_ubuntu_container
root@90416d8418ee:/#
```
> 여기 까지 docker container를 사용하기
--- 
> 여기 부터 docker container에서 작업후 저장하는 방법
```
apt-get update
apt-get install vim

vim my_python.py
> print("my_python")
```

### 8. docker commit -a "jackmappotion" -m "initial_commit_ubuntu" my_ubuntu_container commit_test:latest

```
❯ docker commit -a "jackmappotion" -m "initial_commit_ubuntu" my_ubuntu_container commit_test:latest
sha256:b04c8361e3fd82b4f771d44d384aa529716c72ab944737e0fb74a02fa1d88600

-> 근데 이렇게 하면 나의 dockerhub에 레포지토리를 저장하는것은 불가하다.
```

### 8. docker commit -a "jackmappotion" -m "initial_commit_ubuntu" my_ubuntu_container jackmappotion/practice_dockerhub_init:1.0

```
❯ docker commit -a "jackmappotion" -m "initial_commit_ubuntu" my_ubuntu_container jackmappotion/practice_dockerhub_init:1.0
sha256:f4e61939a8d36e6e67866a0215aa6c07db53b45f1e8c29c100a1e3f7670fab90

이렇게 [user_name]/[image_name]:[tag] 형식으로 해주어야지 이후 push가 가능하다
```

### 9. docker push jackmappotion/practice_dockerhub_init:1.0
```
❯ docker push jackmappotion/practice_dockerhub_init:1.0
The push refers to repository [docker.io/jackmappotion/practice_dockerhub_init]
77cedfe2723e: Pushed
b49483f6a0e6: Pushed
1.0: digest: sha256:3770264620318c9f04e7144e0e650c6e4829178b8625647551dc7468cc5f3a22 size: 741
```

### 10. docker rmi commit_test:latest
```
8 에서 잘못 commit 한 이미지를 삭제한다.

❯ docker rmi commit_test:latest
Untagged: commit_test:latest
Deleted: sha256:b04c8361e3fd82b4f771d44d384aa529716c72ab944737e0fb74a02fa1d88600

추가적으로 push를 완료한 image도 삭제하자
❯ docker rmi jackmappotion/practice_dockerhub_init:1.0
Untagged: jackmappotion/practice_dockerhub_init:1.0
Untagged: jackmappotion/practice_dockerhub_init@sha256:3770264620318c9f04e7144e0e650c6e4829178b8625647551dc7468cc5f3a22
Deleted: sha256:f4e61939a8d36e6e67866a0215aa6c07db53b45f1e8c29c100a1e3f7670fab90
Deleted: sha256:b5733c0142427315d3a6db7ea94553d8b8bc121d99105a4bbb0c0835f20971d8
```

### 11. docker search jackmappotion
```
❯ docker search jackmappotion
NAME                                    DESCRIPTION                 STARS     OFFICIAL   AUTOMATED
jackmappotion/practice_dockerhub_init   checking dockerhub commit   0

내가 push한 image를 확인 가능하다.
```

### 12. docker pull jackmappotion/practice_dockerhub_init:1.0 
```
    - default latest는 따로 지정하지 않아서 오류가 뜨는듯 하다. -
❯ docker pull jackmappotion/practice_dockerhub_init
Using default tag: latest
Error response from daemon: manifest for jackmappotion/practice_dockerhub_init:latest not found: manifest unknown: manifest unknown

    - push 한 이미지 가져오기 -
❯ docker pull jackmappotion/practice_dockerhub_init:1.0
1.0: Pulling from jackmappotion/practice_dockerhub_init
f3f60f415e9a: Already exists
5659b7c6157d: Pull complete
Digest: sha256:3770264620318c9f04e7144e0e650c6e4829178b8625647551dc7468cc5f3a22
Status: Downloaded newer image for jackmappotion/practice_dockerhub_init:1.0
docker.io/jackmappotion/practice_dockerhub_init:1.0
```

### 13. docker rm my_ubuntu_container
```
    - 생성한 컨테이너 삭제 -
❯ docker rm my_ubuntu_container
my_ubuntu_container
```

### 14. docker run -it --name my_ubuntu_container jackmappotion/practice_dockerhub_init:1.0

```
❯ docker run -it --name my_ubuntu_container jackmappotion/practice_dockerhub_init:1.0
root@c69a2757c32c:/# cd home/
root@c69a2757c32c:/home# ls
my_python.py
root@c69a2757c32c:/home#
-- 확인해 보면 이전에 저장한 my_python.py -- 가 잘있다.
```