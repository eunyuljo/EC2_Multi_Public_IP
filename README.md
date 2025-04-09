![Image](https://github.com/user-attachments/assets/93dc420f-0e97-4270-afba-56eb0546a47d)


#### EIP 와 ENI 추가에 따른 확인 

    VyOS를 통한 ENI 추가 구성 
    1. 기본적으로 인스턴스를 시작하는 과정에서 ENI가 미리 Attach 된 상태에서 시작하면 Init 단계에서 처리한다.
    2. 이미 구성된 인스턴스에 추가
    2-1. 추가한 경우라도 DHCP 형태로 연결하는 경우 자동으로 처리
    2-2. STATIC으로 처리하는 경우 작업 진행 
        - Default Routing 에 대한 ECMP 처리 진행
        - 요청에 대한 응답 일관성을 위한 ip routing policy 반영



#### Multi EIP 연결에 따른 PING Drop 

![Image](https://github.com/user-attachments/assets/8d67852e-6b9b-40da-8e35-f9ac10c9fc6d)


    기본적으로 로컬에서 발생한 트래픽이 main routing table만 사용하게 되어있다.
    때문에, EIP로 들어와도 main routing 에 따라 응답하려고 하므로 ping 응답이 안가는 것이다.
    eth1 에 붙은 EIP 로 들어온 요청에 대해 응답도 eth1 로 통해 나가도록 해야한다. 
    따라서, 출발지가 10.0.1.109 면 main이 아니라 table 100 을 조회하도록 조정하는 것이다.