# 🚀 AI/SW 개발 워크스테이션 구축 미션

## 1) 프로젝트 개요
- **미션 목표**: 개발의 시작인 환경 세팅을 직접 수행하며, '재현 가능한 개발 환경' 구축의 원리를 이해합니다.
- **핵심 내용**: 
  - 리눅스 CLI(터미널) 명령어를 통한 디렉토리 및 권한 관리
  - Docker(OrbStack)를 활용한 컨테이너 기반 실행 환경 구축 및 관리
  - Dockerfile을 통한 커스텀 이미지 제작 및 포트 매핑/볼륨 설정
  - Git/GitHub을 활용한 버전 관리 및 소스코드 공유 협업 기반 마련
- **기대 효과**: "내 컴퓨터에서는 되는데?"라는 문제를 해결하고, 팀원 누구나 동일한 환경에서 실행 가능한 워크스테이션 구축 능력을 습득합니다.

### 🌸 솔바오의 이해버전
```text
- 미션 : 나만의 요리 작업대(워크스테이션) 만들기! 🧑‍🍳
- 미션의 핵심: 내가 명령어로 컴퓨터를 조작하고, 그 과정을 기록하는 것
```

### 🌸 시작에 앞서, 내가 앞으로 기술해야할 마크다운 문법 꿀팁
```text
- ### : 제목을 만들 때 , # 개수가 많아질수록 글씨가 작아지는 소제목이 됨 (Max 6개까지 사용할 수 있지만, 보통 가독성을 위해 1개-3개 사용)
- - : 목록을 만들 떄, 앞에 대시 
- **글자** : 볼드체 , 단 코드블록에서는 적용안됨. 왜? 코드블록은 말그대로 코드를 있는 그대로 보여주는 공간이기 때문. (주석활용 #)
- 이모지 : 스마트폰에서 이모지 넣는 거랑 똑같이 , 맥(Control + Command + Space) 단축키로 넣기
- 백틱 ``` 3개 : 코드블록 
```
---

## 2) 실행 환경
- **OS**: 
  ```text
  ProductName:    macOS
  ProductVersion: 15.7.4
  BuildVersion:   24G517

- **Shell**:
  ```text
  /bin/zsh
  ```
- **Terminal**: 
  ```text
  Apple Terminal Version 2.14 (455.1)
  ```
  
- **Docker Version**:
  ```text
  Docker version 28.5.2, build ecc6942
  ```
  
- **Git Version**:
  ```text
  git version 2.53.0
  ```

## 3) 수행 항목 체크리스트
- [x] 터미널 기본 조작 (pwd, ls, mkdir 등)
- [x] 파일 및 디렉토리 권한 변경 실습 (chmod)
- [x] Docker 설치 및 기본 점검 (docker info)
- [ ] 기존 Dockerfile 기반 커스텀 이미지 제작 및 빌드
- [ ] 컨테이너 실행 및 포트 매핑 접속 확인
- [ ] 바인드 마운트 및 Docker 볼륨 영속성 검증
- [ ] Git 사용자 정보 설정 및 GitHub 저장소 연동

## 4) 검증 방법 요약
- **터미널/권한**: `ls -l` 명령어를 통해 변경된 권한 모드(rwx) 확인
- **Docker**: `docker ps`로 컨테이너 실행 상태 확인 및 브라우저 접속 결과 캡처
- **볼륨**: 컨테이너 삭제 후 재실행 시 데이터 유지 여부 확인
- **Git**: `git config --list` 및 GitHub 저장소 커밋 이력 확인

---

## 5) 수행 로그 (명령어 및 출력)

### ① 터미널 조작 및 권한 관리, 파일 및 디렉토리 권한 변경 실습

```bash
#현재 위치 확인, 디렉토리생성(-p 부모님옵션,~/ 절대주소), 디렉토리로이동, 빈파일생성, 파일에대한 권한확인, 권한변경, 바뀐권한확인

greeny10031213@c5r4s7 ~ % pwd
/Users/greeny10031213
greeny10031213@c5r4s7 ~ % mkdir -p ~/codyssey/mission
greeny10031213@c5r4s7 ~ % cd ~/codyssey/mission
greeny10031213@c5r4s7 mission % 
greeny10031213@c5r4s7 mission % cd ~/codyssey/mission
greeny10031213@c5r4s7 mission % touch solbao.txt
greeny10031213@c5r4s7 mission % ls -l
total 0
-rw-r--r--  1 greeny10031213  greeny10031213  0 Apr  2 23:30 solbao.txt
greeny10031213@c5r4s7 mission % chmod 755 solbao.txt
greeny10031213@c5r4s7 mission % ls -l
total 0
-rwxr-xr-x  1 greeny10031213  greeny10031213  0 Apr  2 23:30 solbao.txt
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission %
```

```bash
#현재위치확인, 파일에 내용넣기,파일내용확인, 파일복사, 파일이름바꾸기, 파일삭제, 목록확인(숨긴파일포함), 디렉토리생성(-p옵션없이),권한확인,권한변경,바뀐권한확인 

greeny10031213@c5r4s7 mission % pwd
/Users/greeny10031213/codyssey/mission
greeny10031213@c5r4s7 mission % echo "안녕하세요 솔바오입니다" > solbao.txt
greeny10031213@c5r4s7 mission % cat solbao.txt
안녕하세요 솔바오입니다
greeny10031213@c5r4s7 mission % open.
zsh: command not found: open.
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % cp solbao.txt solbao_copy.txt
greeny10031213@c5r4s7 mission % mv solbao_copy.txt renamed.txt
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % rm renamed.txt
greeny10031213@c5r4s7 mission % ls -la
total 8
drwxr-xr-x  3 greeny10031213  greeny10031213   96 Apr  3 00:42 .
drwxr-xr-x  4 greeny10031213  greeny10031213  128 Apr  2 23:27 ..
-rwxr-xr-x@ 1 greeny10031213  greeny10031213   35 Apr  3 00:39 solbao.txt

greeny10031213@c5r4s7 mission % mkdir test_dir
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % rm test_dir
rm: test_dir: is a directory
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % rm-r test_dir 
zsh: command not found: rm-r
greeny10031213@c5r4s7 mission % rm -r test_dir
greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % ls -l
total 8
-rwxr-xr-x@ 1 greeny10031213  greeny10031213  35 Apr  3 00:39 solbao.txt
greeny10031213@c5r4s7 mission % ls -la
total 24
drwxr-xr-x  4 greeny10031213  greeny10031213   128 Apr  3 02:38 .
drwxr-xr-x  4 greeny10031213  greeny10031213   128 Apr  2 23:27 ..
-rw-r--r--@ 1 greeny10031213  greeny10031213  6148 Apr  3 02:05 .DS_Store
-rwxr-xr-x@ 1 greeny10031213  greeny10031213    35 Apr  3 00:39 solbao.txt
greeny10031213@c5r4s7 mission % mkdir project
greeny10031213@c5r4s7 mission % open
Usage: open [-e] [-t] [-f] [-W] [-R] [-n] [-g] [-h] [-s <partial SDK name>][-b <bundle identifier>] [-a <application>] [-u URL] [filenames] [--args arguments]
Help: Open opens files from a shell.
      By default, opens each file using the default application for that file.  
      If the file is in the form of a URL, the file will be opened as a URL.
Options: 
      -a                    Opens with the specified application.
      --arch ARCH           Open with the given cpu architecture type and subtype.
      -b                    Opens with the specified application bundle identifier.
      -e                    Opens with TextEdit.
      -t                    Opens with default text editor.
      -f                    Reads input from standard input and opens with TextEdit.
      -F  --fresh           Launches the app fresh, that is, without restoring windows. Saved persistent state is lost, excluding Untitled documents.
      -R, --reveal          Selects in the Finder instead of opening.
      -W, --wait-apps       Blocks until the used applications are closed (even if they were already running).
          --args            All remaining arguments are passed in argv to the application's main() function instead of opened.
      -n, --new             Open a new instance of the application even if one is already running.
      -j, --hide            Launches the app hidden.
      -g, --background      Does not bring the application to the foreground.
      -h, --header          Searches header file locations for headers matching the given filenames, and opens them.
      -s                    For -h, the SDK to use; if supplied, only SDKs whose names contain the argument value are searched.
                            Otherwise the highest versioned SDK in each platform is used.
      -u, --url URL         Open this URL, even if it matches exactly a filepath
      -i, --stdin  PATH     Launches the application with stdin connected to PATH; defaults to /dev/null
      -o, --stdout PATH     Launches the application with /dev/stdout connected to PATH; 
          --stderr PATH     Launches the application with /dev/stderr connected to PATH to
          --env    VAR      Add an enviroment variable to the launched process, where VAR is formatted AAA=foo or just AAA for a null string value.

greeny10031213@c5r4s7 mission % open .
greeny10031213@c5r4s7 mission % ls -ld project 
drwxr-xr-x  2 greeny10031213  greeny10031213  64 Apr  3 02:49 project
greeny10031213@c5r4s7 mission % chmod 700 project
greeny10031213@c5r4s7 mission % ls -ld project
drwx------  2 greeny10031213  greeny10031213  64 Apr  3 02:49 project

```
### 🌸① 솔바오의 이해버전
```text
🏗️ 1단계: 터미널과 친해지기 ( 컴퓨터와 대화하기 ! > '마우스 없이 글로 시키는 심부름' )

1. 꼭 알아야 할 기초 명령어

- pwd: "나 지금 어디 있어?" (현재 경로(위치) 확인)
- ls -la: "여기 뭐가 있어? 숨겨진 것도 다 보여줘." 
- mkdir codyssey: "codyssey라는 이름의 새 폴더 만들어."
- cd codyssey: "codyssey 폴더 안으로 들어가."
- touch solbao.txt : "solbao.txt 라는 빈 문서 하나 만들어."
- echo : 파일에 내용 넣기 (요리 재료 넣기!)
- cat : 파일 내용 확인하기
- cp : 파일 복사하기
- mv : 파일 이름 바꾸기
- rm : 파일 삭제하기 (폴더는 -r추가)
- ls -l : 권한 확인하기 (폴더는 -d추가)

2. 권한(Permission) 이해하기

- 파일에는 '읽기(r)', '쓰기(w)', '실행(x)' 권한이 있다. / r=4, w=2, x=1 / 권한이 없다 = - 
- 755 / chmod 755 [파일명] : "나는 다 할 수 있고, 남들은 읽고 실행만 해!"
- 644 / chmod 644 [파일명] : "나는 읽고 쓸 수 있고, 남들은 읽기만 해!"

3. ⭐️파일은 755로 했으나, 디렉토리는 700으로 한이유!
- 보통 맥에서 폴더를 새로 만들면 기본권한이 755인 경우가 많기 때문에, 로그상 변화를 확실히 주기 위해서! rwxr-xr-x > rwx------
- 개발자는 내 소중한 설정파일이나 개인(key)같은 걸 남들이 못보게 숨겨야 할 때가 많기 떄문에, "보안"의 개념을 확실히 확인하기 위해서!
- 파일은 남들도 읽고 실행하게 해주는 755로 (공용권한) , 디렉토리는 나만 들어갈 수 있는 비밀공간 700으로 (개인권한)

```
---

### ② Docker 설치 및 기본 점검

> **솔바오의 이해**: "요리 로봇(Docker)을 깨우고, 마트에서 첫 번째 요리 세트(Hello-world)를 잘 사왔는지 확인하는 과정!"
```bash

# 1. 도커 버전 확인 (⭐️도커 데몬이 실행중이지 않아도 출력 가능)

greeny10031213@c5r4s7 mission % docker --version
Docker version 28.5.2, build ecc6942

# 2. 도커 데몬 상태 확인 ((⭐️도커 데몬이 실행중이어야만 전체 정보 출력 가능))


greeny10031213@c5r4s7 mission % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/greeny10031213/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/greeny10031213/.docker/cli-plugins/docker-compose

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: runc io.containerd.runc.v2
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 78c11bd4-40e9-414d-a75c-43fbfe23c33a
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set

⭐️greeny10031213@c5r4s7 mission % docker info 사실 이 중 중요한 정보는 요 3가지
ClientVersion:    28.5.2 
Server Version: 28.5.2
Operating System: OrbStack

Client Version: 내 도커가 몇 버전인지
Server Version: 연결된 엔진이 몇 버전인지
Operating System: OrbStack(혹은 Linux)인지 확인

# 3. 테스트용 컨테이너 실행

greeny10031213@c5r4s7 mission % docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
```
---
### ② Docker 기본 운영 명령 수행

> **솔바오의 이해**: "마트에 어떤 물건(이미지)이 있는지, 주방에 어떤 요리(컨테이너)가 돌아가는지 감시하기!"
```bash
# 1. 이미지 목록 확인

greeny10031213@c5r4s7 mission % docker images
REPOSITORY       TAG       IMAGE ID       CREATED             SIZE
my-workstation   latest    cf77719ba3d7   About an hour ago   141MB
hello-world      latest    e2ac70e7319a   9 days ago          10.1kB

# 2. 실행 중/전체 컨테이너 목록 확인

greeny10031213@c5r4s7 mission % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

greeny10031213@c5r4s7 mission % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED       STATUS                   PORTS     NAMES
2c0f37efe6ff   hello-world   "/hello"   2 hours ago   Exited (0) 2 hours ago             sweet_robinson

# 3. 컨테이너 운영 상태(리소스) 확인
greeny10031213@c5r4s7 mission % docker stats --no-stream
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS

# 4. 컨테이너 로그 확인 (hello-world 실행 기록)
greeny10031213@c5r4s7 mission % docker logs 2c0f37efe6ff

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
---
### ③ 컨테이너 실행 및 내부 진입 실습

> **솔바오의 이해**: "상자(컨테이너) 안으로 직접 들어가서 심부름 시키기!"
```bash

# 1. Ubuntu 컨테이너 실행 및 내부 진입

greeny10031213@c5r4s7 mission % docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
817807f3c64e: Already exists 
Digest: sha256:186072bba1b2f436cbb91ef2567abca677337cfc786c86e107d25b7072feef0c
Status: Downloaded newer image for ubuntu:latest
root@62e4821a6c05:/# 

# 2. 컨테이너 내부 명령 수행 (컨테이너 안에서 입력)

root@62e4821a6c05:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

root@62e4821a6c05:/# echo "Hello from inside Ubuntu"
Hello from inside Ubuntu

root@62e4821a6c05:/# exit
exit
greeny10031213@c5r4s7 mission %

 💡 [솔바오의 정리] attach vs exec의 차이
- attach: 이미 돌아가고 있는 요리사의 어깨 너머로 작업을 같이 보는 것 (터미널 연결)
- exec: 요리사가 일하는 주방에 새로운 조수를 한 명 더 보내서 따로 일을 시키는 것

```

---
### ③ Dockerfile 기반 커스텀 이미지 제작 및 빌드

> **솔바오의 이해**: "나만의 요리 레시피(Dockerfile)를 적어서, 그대로 요리 세트(이미지)를 만드는 과정!"
```bash

# 1. Dockerfile 내용 확인 (cat 명령어로 내가 적은 레시피 보여주기)

greeny10031213@c5r4s7 mission % cat Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y figlet
CMD ["figlet", "SOLBAO WORKSTATION"]


# 2. 이미지 빌드 실행 (나만의 요리 세트 만들기)

greeny10031213@c5r4s7 mission % docker build -t my-workstation .
[+] Building 0.5s (6/6) FINISHED                                                                     docker:orbstack
 => [internal] load build definition from Dockerfile                                                            0.1s
 => => transferring dockerfile: 141B                                                                            0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                0.0s
 => [internal] load .dockerignore                                                                               0.1s
 => => transferring context: 2B                                                                                 0.0s
 => [1/2] FROM docker.io/library/ubuntu:latest                                                                  0.0s
 => CACHED [2/2] RUN apt-get update && apt-get install -y figlet                                                0.0s
 => exporting to image                                                                                          0.1s
 => => exporting layers                                                                                         0.0s
 => => writing image sha256:cf77719ba3d7b3ff5a224d9885ac41b45185db3f2d8c7ac1e031ecc38e365c1c                    0.0s
 => => naming to docker.io/library/my-workstation    

# 3. 만들어진 이미지 목록 확인

greeny10031213@c5r4s7 mission % docker images
REPOSITORY       TAG       IMAGE ID       CREATED       SIZE
my-workstation   latest    cf77719ba3d7   4 hours ago   141MB
hello-world      latest    e2ac70e7319a   10 days ago   10.1kB
ubuntu           latest    f794f40ddfff   5 weeks ago   78.1MB

# 4. 커스텀 컨테이너 실행 및 결과 확인

greeny10031213@c5r4s7 mission % docker run my-workstation
 ____   ___  _     ____    _    ___  
/ ___| / _ \| |   | __ )  / \  / _ \ 
\___ \| | | | |   |  _ \ / _ \| | | |
 ___) | |_| | |___| |_) / ___ \ |_| |
|____/ \___/|_____|____/_/   \_\___/ 
                                     
__        _____  ____  _  ______ _____  _  _____ ___ ___  _   _ 
\ \      / / _ \|  _ \| |/ / ___|_   _|/ \|_   _|_ _/ _ \| \ | |
 \ \ /\ / / | | | |_) | ' /\___ \ | | / _ \ | |  | | | | |  \| |
  \ V  V /| |_| |  _ <| . \ ___) || |/ ___ \| |  | | |_| | |\  |
   \_/\_/  \___/|_| \_\_|\_\____/ |_/_/   \_\_| |___\___/|_| \_|
```
---
### ④ 컨테이너 실행 및 포트 매핑 접속 확인

> 솔바오의 이해: "만든 요리 세트를 실제로 가동하고, 밖에서 음식을 주문(접속)할 수 있게 창구를 여는 것!"
```bash
💡💫Trouble shooting point
# 1. 컨테이너 실행 (8080포트 등으로 창구 개방)
greeny10031213@c5r4s7 mission % docker run -d -p 8080:80 --name solbao-app my-workstation
docker: Error response from daemon: Conflict. The container name "/solbao-app" is already in use by container "4231c564e91388bb3a6b76f0d6e4aa5e7d5538c0e9541316d191ccdce8c08fc4". You have to remove (or rename) that container to be able to reuse that name.

Run 'docker run --help' for more information

# 2. 실행 중인 컨테이너 상태 확인
greeny10031213@c5r4s7 mission % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

. **figlet은 글자만 보여주고 끝나는 '일회성 도구'**인데, 미션에서는 **'계속 켜져 있는 웹 서버(식당)'**를 원하기 때문이야. 그래서 포트 매핑(창구 열기)을 해도 브라우저에서 볼 게 없는 거지.

[선택 A] 웹 서버 베이스 활용 (추천! ⭐)
솔바오의 선택: Nginx라는 유명한 웹 서버 '이미 만들어진 요리'를 가져와서 내 메뉴판만 바꿨어!

기존 베이스: nginx:alpine (가볍고 빠른 웹 서버 이미지)

커스텀 포인트: 기본 Nginx 페이지 대신 "솔바오의 워크스테이션" 메시지가 뜨는 index.html로 교체
