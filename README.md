# AWS EC2 인스턴스에 도커로 NDP 환경 구축

## EC2

1. EC2 instance 생성
    * 보안그룹에 SSH, HTTP, HTTPS Rule 설정
    * SSH 접속용 프라이빗 키 안전하게 저장
    * EIP 생성 후 instance 와 연결
    
1. SSH 접속 설정
    1. Linux
        * cp ec2-docker-ndp.pem ~/.ssh
        * chmod 600 ~/.ssh/ec2-docker-ndp.pem
        * vim ~/.ssh/config
        ```
        Host ec2-docker-ndp
            HostName {{EIP}}
            User ec2-user
            IdentityFile ~/.ssh/ec2-docker-ndp.pem
        ```
        * chmod 600 ~/.ssh/config
    1. Windows
        * puttygen.exe 로 pem 파일을 ppk 로 변환
        ```
        Conversions > Import Key > Save private key
        ```
        * putty.exe 에 ppk 파일 등록
        ```
        Connection > SSH > Auth
        ```
        * Putty 접속
        ```
        Host : ec2-user@{{EIP}}
        ```
    > SSH 접속 : ssh ec2-docker-ndp

1. EC2 Linux 설정
    * Java 8 설치
    ```
    sudo yum list | grep java-1.8
    sudo yum install java-1.8.0-openjdk-devel.x86_64
    
    sudo /usr/sbin/alternatives --config java
    sudo yum remove java-1.7.0-openjdk
    ```
    * 타임존 변경
    ```
    sudo rm /etc/localtime
    sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
    ```
    * Locale 변경
    ```
    sudo vi /etc/sysconfig/i18n
    LANG=ko_KR.UTF-8
    
    source /etc/sysconfig/i18n
    ```
    > locale -a 로 ko_KR.UTF-8 이 안보일때는 설치가 필요
    > locale-gen ko_KR.UTF-8 또는 localedef -f UTF-8 -i ko_KR ko_KR.UTF-8
    
    * Hostname 변경
    ```
    # HOSTNAME 변경
    sudo vim /etc/sysconfig/network
    
    # hosts 파일 수정
    sudo vim /etc/hosts
    127.0.0.1    HOSTNAME
    
    # 재부팅
    sudo reboot
    ```
    
## Docker

1. Install Docker on EC2
    ```
    sudo yum update -y
    sudo yum install docker.x86_64
    sudo service docker start
    sudo usermod -a -G docker ec2-user
    ```
    > SSH 재접속 또는 docker restart 후 docker ps 확인
        
