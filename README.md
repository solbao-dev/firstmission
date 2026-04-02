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
- **미션**: 나만의 요리 작업대(워크스테이션) 만들기! 🧑‍🍳
- **미션의 핵심**: 내가 명령어로 컴퓨터를 조작하고, 그 과정을 기록하는 것
```


### 🌸 시작에 앞서, 내가 앞으로 기술해야할 마크다운 문법 꿀팁
```text
- ###: 제목을 만들 때 , # 개수가 많아질수록 글씨가 작아지는 소제목이 됨 (Max 6개까지 사용할 수 있지만, 보통 가독성을 위해 1개-3개 사용)
- **-**: 목록을 만들 떄, 앞에 대시 
- **(글자)**: 강조하고 싶은 글자 **굵게** 만들기 , 글자 양옆에, 앞뒤로 별표 두개를 붙이면 굵은글씨!
- **이모지**: 스마트폰에서 이모지 넣는 거랑 똑같이 , 맥(Control + Command + Space) 단축키로 넣기
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
- [ ] Docker 설치 및 기본 점검 (docker info)
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

### ① 터미널 조작 및 권한 관리

```bash
현재 위치 확인, 폴더생성, 폴더로이동, 문서생성, 생성한📋"문서"에대한 권한확인, 권한변경, 바뀐권한확인

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

### 🌸① 솔바오의 이해버전
```text
🏗️ 1단계: 터미널과 친해지기 ( 컴퓨터와 대화하기 ! > '마우스 없이 글로 시키는 심부름' )

1. 꼭 알아야 할 기초 명령어

- pwd: "나 지금 어디 있어?" (현재 경로(위치) 확인)
- ls -la: "여기 뭐가 있어? 숨겨진 것도 다 보여줘." 
- mkdir codyssey: "codyssey라는 이름의 새 폴더 만들어."
- cd codyssey: "codyssey 폴더 안으로 들어가."
- touch solbao.txt : "solbao.txt 라는 빈 문서 하나 만들어."

2. 권한(Permission) 이해하기

- 파일에는 '읽기(r)', '쓰기(w)', '실행(x)' 권한이 있다.
- 755 / chmod 755 [파일명] : "나는 다 할 수 있고, 남들은 읽고 실행만 해!"
- 644 / chmod 644 [파일명] : "나는 읽고 쓸 수 있고, 남들은 읽기만 해!"

```
