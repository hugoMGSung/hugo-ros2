# ROS2 튜토리얼

## ROS2 입문

### 라즈베리파이 ROS2 설치

라즈베리파이 5에서는 라즈비안에 ROS2 설치도 가능합니다만, 설치 도중 오류가 많이 발생하고 해결하는데 어려움이 있습니다.
따라서, Ubuntu 26으로 진행합니다.


#### 개발도구 설치

```bash
sudo apt install -y \
git curl wget vim nano htop tree unzip zip \
build-essential cmake ninja-build pkg-config
```

- 파이썬 설치 확인을 하고 넘어갑니다.

#### ROS2 Jazzy 설치

아래의 순서대로 진행합니다.

##### 워크스페이스 생성

```bash
mkdir -p ~/ros2_jazzy/src

cd ~/ros2_jazzy
```

##### 개발환경 설치

```bash
sudo apt install -y \
build-essential \
cmake \
git \
python3-pip \
python3-venv \
python3-colcon-common-extensions \
python3-rosdep \
python3-vcstool \
python3-dev \
python3-empy \
python3-numpy \
python3-lark \
python3-setuptools \
python3-yaml \
python3-pytest \
curl \
wget
```

위와 같이 설치하면, 설치중 아래와 같은 오류가 발생합니다.

```bash
...
Error: python3-colcon-common-extensions 패키지를 찾을 수 없습니다 
Error: python3-rosdep 패키지를 찾을 수 없습니다 
Error: python3-vcstool 패키지를 찾을 수 없습니다
```

이는 Ubuntu와 달리 Raspbian Trixie에 위의 패키지가 없기 때문입니다.

```bash
$ sudo apt install python3-rosdep2
# 우선설치
$ sudo apt install vcstool

$ sudo apt install -y \
python3-pip \
python3-venv \
python3-colcon-core \
python3-colcon-cmake \
python3-colcon-package-information \
python3-colcon-library-path \
python3-colcon-python-setup-py \
python3-colcon-recursive-crawl \
python3-colcon-test-result


```

그다음 Python 패키지를 추가 설치합니다.

```bash
$ pip3 install -U vcstool rosdep
```


##### ROS2 소스 다운로드

```bash
$ cd ~/ros2_jazzy

$ curl -sSL https://raw.githubusercontent.com/ros2/ros2/jazzy/ros2.repos | vcs import src

```

#### rosdep 초기화

```bash
$ sudo rosdep init
## 이미 초기화되어  있다면,
$ rosdep update
```


##### 의존성 설치

```bash
$ rosdep install \
--from-paths src \
--ignore-src \
-r \
-y
```

위 설치 중 아래의 에러가 납니다.

```bash
ERROR: the following rosdeps failed to install 
 apt: command [sudo -H apt-get install -y python3-sip-dev] failed 
 apt: command [sudo -H apt-get install -y python3-vcstool] failed 
 apt: Failed to detect successful installation of [python3-sip-dev]
 apt: Failed to detect successful installation of [python3-vcstool]
```

**Trixie에서 패키지 이름이 바뀌었거나 사라져서 생기는 문제**입니다.


##### 컴파일

```bash
$ cd ~/ros2_jazzy

$ colcon build \
--symlink-install
```

366개 패키지가 설치되어야 합니다. 2시간 이상의 시간이 걸리므로 여유를 가지고 진행합니다.