# CentOS 7 에서 Docker 실행하기

## Install Docker

    ```
    sudo yum update -y
    sudo yum install docker.x86_64
    sudo service docker start
    ```

Docker 설치 후 ```docker ps``` 로 확인해 보면 다음과 같은 권한 오류가 발생한다.

    ```
    Got permission denied while trying to connect to the Docker daemon  ...
    ```

## Add user to the docker group

Docker 를 설치하면 ```dockerroot``` 그룹이 생성된다. 현재 유저를 해당 그룹에 멤버로 추가하자.

    ```
    usermod -aG dockerroot $ROOT
    ```

## Docker Daemon socket 이 dockerroot 그룹으로 실행되도록 수정

/etc/docker/daemon.json 을 수정한다.

   ```
   {
       "live-restore" : true,
       "group" : "dockerroot"
   }
   ```

## Docker Restart 

   ```
   sudo service docker restart
   ```

## 재접속하여 확인

   ```
   docker ps
   ```

## References
  * https://coderleaf.wordpress.com/2017/02/10/run-docker-as-user-on-centos7/
  
