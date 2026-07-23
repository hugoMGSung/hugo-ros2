# ROS2 튜토리얼

## ROS2 입문

### ROS 개요

#### ROS가 필요한 이유

일반 프로그램의 경우

```markdown
Sensor
   ↓
Program
   ↓
Motor
```

하나의 프로그램이나 2중 레이어 상태에서 모든 기능을 수행합니다.
보통의 경우 아두이노 IoT와 라즈베리파이로 연결을 하고 C#/Python 등의 모니터링 앱에서 MQTT 등으로 `센서에서 센싱된 데이터`를 Subscribe로 확인, 다시 MQTT로 모터룰 동작시킬 Publish로 전송, `모터를 동작`시킵니다.

이때 문제점은,

- 유지보수 어려움
- 기능 추가 어려움
- 여러 명 개발 어려움

등이 있죠.

이를 ROS로 개발한다면,

```markdown
Camera Node
        ↓
Image Topic
        ↓
AI Node
        ↓
Result Topic
        ↓
Robot Node
```

와 같이 기능별로 프로그램을 분리할 수 있습니다.

#### ROS의 특징

ROS는 `DDS`(Data Distribution Service)기반의 통신으로 실시간성이 뛰어나고, OS 멀티플랫폼을 지원하고, Multi Robot을 연결할 수 있습니다.
ROS는 버전 1과 2가 있으며, 둘의 차이는 아래와 같습니다.


| ROS1        | ROS2          |
| ----------- | ------------- |
| Master 필요 | Master 없음   |
| TCPROS      | DDS           |
| Ubuntu 중심 | 멀티 플랫폼   |
| 보안 약함   | Security 지원 |

### OS Ubuntu 설정

#### Ubuntu 사용이유

ROS2 최신 버전은 2026년 5월 기준 ROS2 Lyrical Luth이고 Ubuntu 26.04 를 지원합니다. 다만, 신규 배포판은 교육자료와 패키지 호환성 문제로 사용이 어려울 수 있습니다.


| 구분          | 환경                          | 용도                      |
| ------------- | ----------------------------- | ------------------------- |
| 안정적인 강의 | `Ubuntu 22.04 + ROS 2 Humble` | 기존 자료와 예제가 풍부함 |
| 중간 단계     | Ubuntu 24.04 + ROS 2 Jazzy    | -                         |
| 최신 과정     | Ubuntu 26.04 + ROS 2 Lyrical  | 장기 운영 과정            |
| 시뮬레이터    | -                             | 모바일 로봇·센서 실습    |
| 개발 언어     | Python 중심, C++ 비교         | 입문 난이도 완화          |
| 도구          | VS Code, RViz2, rqt, colcon   | 개발·시각화·빌드        |

ROS2 버전에 맞는  Ubuntu를 설치, 사용하면 됩니다.

#### Ubuntu 22.04 Desktop 설치

https://ubuntu.com/download/desktop 에서 최신 버전을 설치하거나 또는 이전 버전도 설치할 수 있습니다. 하지만, 22.04 버전을 찾아 다운로드 하고자 하면, https://ftp.kaist.ac.kr/ubuntu-cd/ 에서 이전 버전을 찾아 다운로드 하는 것을 추천합니다.

![](assets/20260723_193439_image.png)

https://releases.ubuntu.com/22.04/ 여기가 가장 Official 사이트입니다.

##### PC에 직접 설치

USB 메모리(8GB 이상)를 이용하면 됩니다.

Ubuntu 22.04 ISO를 [Rufus](https://rufus.ie/ko/)를 통해서 USB에 저장합니다.

설치 순서는 다음과 같습니다.

- Rufus로 Ubuntu 부팅 USB 생성
- BIOS/UEFI에서 USB로 부팅
- **Install Ubuntu** 선택
- 설치 유형 선택
  - **Install Ubuntu alongside Windows**: Windows와 듀얼 부팅(권장)
  - **Erase disk and install Ubuntu**: 디스크 전체 삭제 후 Ubuntu만 설치(주의)
- 사용자 계정 생성
- 설치 완료 후 재부팅

처음 부팅 시 GRUB 메뉴에서 Windows와 Ubuntu 중 원하는 운영체제를 선택할 수 있습니다.

윈도우에서 설치할 때는 제어판에서 디스크 관리로 진입, 현재 설치된 C: 드라이브에서 오른쪽 버튼, `볼륨 축소`를 선택합니다.

![](assets/20260723_193542_image.png)

다음으로 축소 창에서 아래와 같이 축소할 공간 입력(MB) 를 입력해줍니다. 아래의 71680은 70GB를 뜻합니다. PC에 설치할 때는 이 정도는 잡을 것을 추천합니다. Ubuntu 22.04는

![](assets/20260723_193553_image.png)

축소 후 아래와 같이 됩니다.

![](assets/20260723_193601_image.png)

USB 우선 부팅으로 CMOS를 변경 후 재부팅되면 아래의 선택 화면이 뜹니다.

![](assets/20260723_193619_image.png)

##### Virtual Box Ubuntu 설치

![](assets/20260723_193628_image.png)


`새로 만들기` 를 클릭합니다.

![](assets/20260723_193636_image.png)


위와 같이 작성하고 `다음`을 누릅니다. 무인설치 건터뛰기를 해서 직접 설정해보는 게 좋습니다.

![](assets/20260723_193642_image.png)


필요한 경우 입력합니다.

![](assets/20260723_193647_image.png)


하드웨어는 메모리 최소 4096MB, 권장 8196MB. 프로세서sms 최소 2 Core, 권장 4 Core를 설정합니다.

![](assets/20260723_193653_image.png)


하드 디스크는 70GB를 권장합니다. 가상 머신 만들기 요약을 확인 후 완료를 클릭합니다.

클릭해서 부팅합니다.

![](assets/20260723_193658_image.png)


Try of Install Ubuntu를 선택합니다.

![](assets/20260723_193703_image.png)


넘어간 뒤 설치 시작 화면으로 넘어갑니다. 한국어를 선택합니다.

![](assets/20260723_193717_image.png)


키보드 레이아웃을 Korean 101/104로 선택합니다.

![](assets/20260723_193722_image.png)


일반 설치 로 진행합니다.

![](assets/20260723_193727_image.png)


설치형식을 기타로 합니다.

![](assets/20260723_193735_image.png)


PC에 설치할 경우는 나눈 파티션이 비어있는 영역 `남은 공간`이 있습니다. 여기를 새 파티션 만들기로 `/` 를 입력하고 새로 만든 파티션을 선택해서 진행하면 되고, Virtual Box라면 아래와 같이 하나로 되어 있습니다. 이를 그냥 사용하면 됩니다.

![](assets/20260723_193746_image.png)


나머지는 설치지역 Seoul, 다음이 계정입니다. 아래의 화면에서 자신의 계정을 입력합니다.

![](assets/20260723_193751_image.png)


설치를 진행합니다.

![](assets/20260723_193756_image.png)


완료 되었습니다.

![](assets/20260723_193802_image.png)


24.04.4 LTS 버전으로 업그레이드 하면 안됩니다. `업그레이드하지 않음` 을 클릭하세요. 아래 소프트웨어 업데이터는 진행해도 됩니다.

![](assets/20260723_193807_image.png)


#### 한글 설정

한글은 사용하되 Default Language를 영어로 해서 폴더명이 한글로 생성되지 않게 주의합니다.

Settings(설정)로 진입합니다. Region and Language(지역 및 언어)에서 언어를 추가하면 됩니다.

![](assets/20260723_193813_image.png)


재부팅 해서, 폴더명을 영어로 변경해줍니다.

![](assets/20260723_193823_image.png)


키보드는 현재 한글입니다. 키보드는 Korean(Hangul) 로 올려놓고, English를 추가합니다.

![](assets/20260723_193829_image.png)


Setup을 클릭합니다.

![](assets/20260723_193834_image.png)


한영키를 누르면 Alt_R 로 표시됩니다. OK를 누릅니다.

![](assets/20260723_193840_image.png)


한글 영어가 잘 전환됩니다.

![](assets/20260723_193845_image.png)


#### Ubuntu 컴퓨터명 변경

호스트명이 hugosung-VirtualBox로 너무 깁니다. 아래의 명령어로 조금 짧게 변경합니다.

```bash
> sudo hostnamectl set-hostname ros-ubuntu
```

#### 최초 명령어

리눅스를 시작하고 제일 먼저 입력하는 명령어는 아래와 같습니다. OS 자체의 필요 패키지들을 최신버전으로 변경하는 명령어입니다.

```bash
> sudo apt-get update
> sudo apt-get upgrade
```

### ROS 필요 설정

#### 터미네이터 설치

기존의 Terminal 보다 사용하기 편리한 터미널 애플리케이션입니다.

```bash
> sudo apt-get install terminator
```

#### 알아야 할 리눅스 명령어

##### 기본 명령어


| 명령어    | 설명                         | 예제                    |
| --------- | ---------------------------- | ----------------------- |
| `pwd`     | 현재 작업 중인 디렉터리 출력 | `pwd`                   |
| `ls`      | 파일 및 폴더 목록 보기       | `ls`                    |
| `ls -l`   | 상세 정보 출력               | `ls -l`                 |
| `ls -a`   | 숨김 파일 포함 출력          | `ls -a`                 |
| `cd`      | 디렉터리 이동                | `cd Documents`          |
| `cd ..`   | 상위 디렉터리 이동           | `cd ..`                 |
| `cd ~`    | 홈 디렉터리 이동             | `cd ~`                  |
| `mkdir`   | 디렉터리 생성                | `mkdir test`            |
| `rmdir`   | 빈 디렉터리 삭제             | `rmdir test`            |
| `rm`      | 파일 삭제                    | `rm file.txt`           |
| `rm -r`   | 디렉터리 삭제                | `rm -r test`            |
| `cp`      | 파일 복사                    | `cp a.txt b.txt`        |
| `cp -r`   | 디렉터리 복사                | `cp -r dir1 dir2`       |
| `mv`      | 파일 이동 또는 이름 변경     | `mv a.txt b.txt`        |
| `touch`   | 빈 파일 생성                 | `touch test.txt`        |
| `cat`     | 파일 내용 출력               | `cat hello.txt`         |
| `less`    | 페이지 단위로 파일 보기      | `less hello.txt`        |
| `head`    | 파일 앞부분 출력             | `head hello.txt`        |
| `tail`    | 파일 뒷부분 출력             | `tail hello.txt`        |
| `tail -f` | 로그 실시간 확인             | `tail -f log.txt`       |
| `clear`   | 터미널 화면 지우기           | `clear`                 |
| `history` | 명령어 사용 기록             | `history`               |
| `find`    | 파일 검색                    | `find . -name "*.txt"`  |
| `grep`    | 문자열 검색                  | `grep "hello" file.txt` |
| `which`   | 실행 파일 위치 확인          | `which python3`         |
| `echo`    | 문자열 출력                  | `echo Hello`            |
| `man`     | 명령어 도움말                | `man ls`                |

##### 사용자 및 권한


| 명령어   | 설명             | 예제                            |
| -------- | ---------------- | ------------------------------- |
| `whoami` | 현재 사용자 확인 | `whoami`                        |
| `passwd` | 비밀번호 변경    | `passwd`                        |
| `sudo`   | 관리자 권한 실행 | `sudo apt update`               |
| `chmod`  | 권한 변경        | `chmod 755 file.sh`             |
| `chown`  | 소유자 변경      | `sudo chown user:user file.txt` |

##### 시스템 관리용


| 명령어        | 설명                       | 예제                |
| ------------- | -------------------------- | ------------------- |
| `hostname`    | 컴퓨터 이름 확인           | `hostname`          |
| `hostnamectl` | 호스트 이름 및 시스템 정보 | `hostnamectl`       |
| `df -h`       | 디스크 사용량 확인         | `df -h`             |
| `du -sh`      | 폴더 크기 확인             | `du -sh Downloads`  |
| `free -h`     | 메모리 사용량 확인         | `free -h`           |
| `top`         | 실시간 프로세스 확인       | `top`               |
| `htop`        | 향상된 프로세스 관리       | `htop`              |
| `ps`          | 실행 중인 프로세스         | `ps -ef`            |
| `kill`        | 프로세스 종료              | `kill 1234`         |
| `reboot`      | 시스템 재부팅              | `sudo reboot`       |
| `shutdown`    | 시스템 종료                | `sudo shutdown now` |

##### 패키지 관리

apt와 apt-get은 동일합니다.


| 명령어                 | 설명                   | 예제                   |
| ---------------------- | ---------------------- | ---------------------- |
| `apt update`           | 패키지 목록 업데이트   | `sudo apt update`      |
| `apt upgrade`          | 설치된 패키지 업데이트 | `sudo apt upgrade -y`  |
| `apt install`          | 프로그램 설치          | `sudo apt install git` |
| `apt remove`           | 프로그램 삭제          | `sudo apt remove git`  |
| `apt autoremove`       | 불필요한 패키지 삭제   | `sudo apt autoremove`  |
| `apt search`           | 패키지 검색            | `apt search python3`   |
| `apt list --installed` | 설치된 패키지 목록     | `apt list --installed` |

##### 네트워크


| 명령어    | 설명               | 예제                                |
| --------- | ------------------ | ----------------------------------- |
| `ip addr` | IP 주소 확인       | `ip addr`                           |
| `ping`    | 네트워크 연결 확인 | `ping google.com`                   |
| `curl`    | 웹 요청            | `curl https://google.com`           |
| `wget`    | 파일 다운로드      | `wget https://example.com/file.zip` |
| `ssh`     | 원격 접속          | `ssh user@192.168.0.10`             |

##### 압축


| 명령어      | 설명           | 예제                            |
| ----------- | -------------- | ------------------------------- |
| `zip`       | 압축           | `zip test.zip *.txt`            |
| `unzip`     | 압축 해제      | `unzip test.zip`                |
| `tar -cvf`  | tar 파일 생성  | `tar -cvf backup.tar test/`     |
| `tar -xvf`  | tar 파일 해제  | `tar -xvf backup.tar`           |
| `tar -czvf` | gzip 압축      | `tar -czvf backup.tar.gz test/` |
| `tar -xzvf` | gzip 압축 해제 | `tar -xzvf backup.tar.gz`       |

##### 개발자 용


| 명령어              | 설명             | 예제                |
| ------------------- | ---------------- | ------------------- |
| `git --version`     | Git 버전 확인    | `git --version`     |
| `python3 --version` | Python 버전 확인 | `python3 --version` |
| `code .`            | VS Code 실행     | `code .`            |
| `nano`              | 터미널 편집기    | `nano test.txt`     |
| `vim`               | Vim 편집기       | `vim test.txt`      |

##### 터미널 단축키


| 단축키     | 설명                    |
| ---------- | ----------------------- |
| `Tab`      | 자동완성                |
| `↑ / ↓`  | 이전 명령어             |
| `Ctrl + C` | 실행 중인 프로그램 종료 |
| `Ctrl + Z` | 작업 일시정지           |
| `Ctrl + L` | 화면 지우기             |
| `Ctrl + R` | 명령어 검색             |
| `Ctrl + D` | 터미널 종료             |
| `Ctrl + A` | 줄의 처음으로 이동      |
| `Ctrl + E` | 줄의 끝으로 이동        |
