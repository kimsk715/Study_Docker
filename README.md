# Study_Docker

- VMware

### VMware를 사용하는 이유 : Windows 환경에서 Linux를 설치 및 사용하기 위해서.

### Guest OS : 가상 OS

#### 가상 머신(Virtual Machine) 

	하드 디스크 파일을 멀티 파일로 지정할 경우 파일이 여러 개로 저장되므로, 사용할 때 분산 저장되고 속도도 빠름.
 	
  	.vmdk : 디스크 파일
	.vmxf : 환경설정 파일

윈도우, 리눅스, 네트워크 --> 가상화 --> 클라우드 서비스


#### docker 설치

 	아래와 같은 명령어를 작성하거나,
	sudo dnf -y install dnf-plugins-core
	sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
	sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

	일련의 과정이 포함된 shell 파일을 다운로드 및 실행하는 명령어를 사용하여 설치할 수 있음.
	curl -fsSL https://get.docker.com -o get-docker.sh
	sudo sh ./get-docker.sh --dry-run


	rpm -qa | egrep "docker|containerd"
	yum repolist
	systemctl enable --now docker

	systemctl status docker




VMware의 단점 (가상 머신 환경)
- 준비 시간이 길다(일일히 설치)
- 용량이 크다(배포 시간 오래 걸림)
- 운영체제가 너무 많다
- 가상 머신 개수에 비례해서 하드웨어 리소스 소모량이 큼.

장점
- 서버가 각각 독립적이기 때문에, 서로 영향을 끼치지 않음.

컨테이너 환경
- 각 서버 별 운영체제가 필요 없음.(용량이 작음)
- 각 서버가 리눅스의 프로세스로서 작동함.
- 각 애플리케이션의 파일과 디렉토리만 존재.(용량이 작음)
- 컨테이너가 많아도 하드웨어 리소스 소모량이 적음.
- 용량이 작기 때문에 배포가 편리
- 다만 완벽히 독립적인 시스템이 아니기 때문에, 네임스페이스 기능을 활용해야 됨.

하드웨어		물리적인 장치
소프트웨어 	논리적인 장치(OS, 응용 프로그램)
운영체제		커널 : 프로세스 관리, 메모리 관리, 입출력 관리, 시스템 콜 담당.
			시스템 프로그램 : 쉘(사용자와 커널 간의 대화가 가능하도록 하는 기능 수행)

실제 업무 환경에서는 중간 guest OS 없이 리눅스 안에 바로 애플리케이션 존재.

도커 서버
- 도커 클라이언트 명령을 전달받아서 이미지, 컨테이너, 볼륨, 네트워크 등을 관리하는 데몬을 수행.

2시 40분 전후.
이미지
- 컨테이너를 생성 및 구동하기 위한 읽기 전용 템플릿.
- 컨테이너를 구동하기 위한 실행 파일과 설정 파일의 세트이며, 운영체제(커널)는 포함되어 있지 않음.
- 직접 제작도 가능하고, 로컬에 이미지가 없을 경우에는 도커 레지스트리로부터 다운로드 가능.

레지스트리
- 컨테이너 이미지를 보관하는 저장소
- 도커는 기본적으로 도커 허브에 있는 이미지를 다운로드 받도록 설정되어 있다.

볼륨
- 컨테이너의 데이터를 호스트에 저장하여 보관할 수 있는 마운트 기능.

네트워크
- 같은 네트워크 환경에서 컨테이너 간에 통신이 가능하도록 네트워트 기능을 제공.
- 또한, 


네임스페이스 & cgroup (리눅스 커널 기능)

1) 네임스페이스
- 특정 프로세스를 다른 프로세스로부터 분리시켜 같은 네임스페이스 내에서만 접근할 수 있도록 제한하는 기능.
- 네임스페이스를 이용하여 컨테이너가 하나의 독립된 서버처럼 동작할 수 있게 한다.

2) cgroup

- 컨트롤 그룹이며, 프로세스별로 CPU 및 메모리 사용량과 같은 자원을 감시하고 제한하는 기능.

nginx 이미지 
데비안 리눅스 + nginx 설치 --> 상당히 간단함.


Red Hat 계열 : CentOS, Fedora, Rocky, Amazon, Oracle
Debian 계열 : Ubuntu

이미지 - config - cmd - bash ==> bash shell이 실행.
nginx -g daemon off --> nginx 웹 서버를 백그라운드에서 실행하겠다는 것을 의미.

docker image tag (이미지명) (원하는 이름 or dockerhub ID/이름) --> 이름 및 태그를 변경할 수 있지만, 이미지 개수는 그대로.

출발지 ip 주소 기반 : 6시간 100번 다운로드 가능.

계정 기반 : 6시간 200번 다운로드 가능. ==> docker login -u 아이디

run 옵션 :
--rm : exit 할 때, container도 삭제.
-i : 명령어 작성 시 반응형이 되도록 실행하는 옵션 
-t : 터미널도 실행되도록 하는 옵션.
-d(--detach) : 


bash
-> gnome-system-monitor 실행 --> bash shell 사용 불가능 --> foreground(포그라운드)
-> 종료하면 터미널 사용 가능.

-> gnome-system-monitor & --> bash shell도 동시에 사용 가능 --> 백그라운드 실행. 

