# AWS EC2 인스턴스에 도커로 NDP 환경 구축

## EC2

1. EC2 instance 생성
    * 보안그룹에 SSH, HTTP, HTTPS Rule 설정
    * SSH 접속용 프라이빗 키 안전하게 저장
    * EIP 생성 후 instance 와 연결
    
1. SSH 접속 설정
    * cp ec2-docker-ndp.pem ~/.ssh
    * chmod 600 ~/.ssh/ec2-docker-ndp.pem
    * vim ~/.ssh/config
    ```
    Host ec2-docker-ndp
        HostName {{EIP}}                                                                                                   
        User ec2-user                                                                                                           
        IdentityFile ~/.ssh/ec2-docker-ndp.pem   
    ```
    
