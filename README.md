### DockerFile과 기본 명령어
  
  ex) dockerfile
```dockerfile
FROM python:3.8.5-alpine
ENV PYTHONUNBUFFERED 1

RUN mkdir /code
WORKDIR /code

RUN mkdir src
RUN python3 -m venv venv
 
COPY requirements.txt /code/
RUN pip install -r requirements.txt

COPY src/ /code/src/
```
-  dockerfile은 docker build시에 사용한다. 아래 명령어들이 실행된 docker image가 생성됨!  
        

- 1.FROM  
    - 베이스 이미지(OS) 지정. 
    - 이미 만들어진 다양한 베이스 이미지는 Docker hub에서 확인가능. 


- 2.MAINTAINER   

    - Dockerfile을 관리하는 사람의 이름 또는 이메일 정보 작성. 
    - 빌드에 딱히 영향이 없음.

- 3.COPY    
  
    - 파일이나 디렉토리를 이미지를 복사하며 일반적으로 소스를 복사하는 데 사용.​ 
    - target디렉토리가 없다면 자동으로 생성한다

- 4.ADD  
​   
    - COPY명령어와 매우 유사하나 몇가지 추가 기능이 있습니다. 
    
    - src에 파일 대신 URL을 입력할 수 있고​ src에 압축 파일을 입력하는 경우 자동으로 압축을 해제하면서 복사 가능

- 5.RUN  
​   
    - 가장 많이 사용하는 구문으로 명령어를 그대로 실행한다
    
    - 내부적으로 /bin/sh -c 뒤에 명령어를​ 실행하는 방식

- 6.CMD
​   
    - 도커 컨테이너가 실행되었을 때 실행되는 명령어를 정의.

    - 빌드할 때는 실행되지 않으며 여러 개의 CMD가​ 존재할 경우 가장 마지막 CMD만 실행

    - 한꺼번에 여러 개의 프로그램을 실행하고 싶은 경우에는 run.sh​ 파일을 작성하여 데몬으로 실행

- 7.WORKDIR
​   
    - RUN, CMD, ADD, COPY등이 이루어질 기본 디렉토리를 설정

    - 각 명령어의 현재 디렉토리는 한 줄마다​ 초기화되기 때문에 RUN cd /path를 하더라도 다음 명령어에선 위치가 초기화

    - 같은 디렉토리에서​ 계속 작업하기 위해서 WORKDIR을 사용합니다

- 8.EXPOSE
​   
    - 도커 컨테이너가 실행되었을 때 요청을 기다리고 있는(Listen) 포트를 지정합니다. 

    - 여러개의 포트를 지정할 수​ 있습니다.

- 9.VOLUME
​   
    - 컨테이너 외부에 파일시스템을 마운트 할 때 사용

    - 반드시 지정하지 않아도 마운트 할 수 있지만,​ 기본적으로 지정하는 것이 좋음

- 10.ENV
​   
    - 컨테이너에서 사용할 환경변수를 지정

    - 컨테이너를 실행할 때 -e옵션을 사용하면 기존 값을 오버라이딩​


  ### 도커 기본 명령어

> Dockerfile을 만들어 봤으니 Docker를 실행 시켜 사용해 봐야한다. 
> 그전에 간단한 기본 명령어에 대해 알아야한다 

|옵션|설명|
|---|---|
|-d|백그라운드 모드|
|-p|호스트와 컨에티너의 포트 연결|
|-v|호스트와 컨테이너의 디렉토리 연결|
|-e|컨테이너 내에서 사용할 환경변수 설정|
|-name|컨테이너 이름 설정|
|-rm|프로세스 종료시 컨테이너 자동 제거|
|-it|-i와 -t를 동시에 사용한 것으로 터미널 입력 위한 옵션|
|link|컨테이너 연결|

- 도커 파일을 이미지화 시키기 

```Docker
docker build [OPTIONS] PATH | URL | -
```
> 예시 : Docker 파일 이름을 app이라고 가정
> Docker build --tag appImage ./app   
  

### 중요 사용 방법  
- [ubuntu에서 docker 설치하기](https://docs.docker.com/engine/install/ubuntu/)
    - ubuntu 환경에서 도커 설치하는 방법! 다 적기엔 너무 길다. 시키는대로 하면 되더라.
  
- [docker 관리자 권한 부여](https://blusky10.tistory.com/359)  
    - 도커에 관리자 권한을 부여하여 sudo 없이 docker를 사용 가능.  
    
- ```docker exec -it {container name} /bin/bash```
    - 위의 명령어를 사용하면 container에 들어갈 수 있다. 
    - 그렇지만 왜 /bin/bash를 해야 접속 할 수 있는지는 자세히 모르겠음.  
- ```docker stop {container name} && docker rm {container name}```  
    - container 정지 & 삭제 명령어  
    - container 이름을 정해주는 것이 exec할때도 그렇고 stop rm할때 모두 편리하고 쉬웠음.  
- 기본적인 환경설정을 해줄 shell script가 있으면 매우매우 편하다.  
- ```docker bulid```는 docker image를 만드는 것! 실행은 ```docker run```으로 한다~   
  
일단은 여기까지!
  