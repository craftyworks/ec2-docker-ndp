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
            
        
1. SSH 접속
    * ssh ec2-docker-ndp
    
    
