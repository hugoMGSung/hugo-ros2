# ROS2 튜토리얼

## ROS2 입문

### ROS Humble 설치

- 라즈베리파이 5 모델은 우분투 22.04가 공식 지원되지 않으므로 우분투 24.04 권장
- 24.04의 경우 ROS2 Jazzy로 진행됨

[https://docs.ros.org/en/humble/](https://docs.ros.org/en/humble/) 사이트를 찾아갑니다.

아래의 순서대로 설치하면 됩니다.

#### 로케일 설정

```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```

위와 같이 입력한 뒤 우분투를 재시작합니다. 재시작후 `locale`을 확인하면 모두 `en_US.UTF-8` 로 변경된 것을 확인할 수 있습니다.


#### 소스 셋업

우분투 유니버스 리포지토리를 설치, 설정합니다.

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```
