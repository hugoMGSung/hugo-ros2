# ROS2 튜토리얼

## ROS2 기본 학습

### 학습 순서

* ROS 개념 알아보기
* ROS와 turtlesim
* ROS 프레임워크의 메인 통신 요소
* 로그를 통한 인트로스펙션
* 런치파일 사용법
* 데이터 기록 및 재생법

### ROS 개념

ROS(Robot Operating System)는 로봇 애플리케이션의 구축, 배포, 실행 및 유지 관리를 위한 프레임워크, 도구 및 라이브러리를 제공하는 오픈 소스 생태계를 뜻합니다.

물류 분야에서는 내비게이션, 지도 작성, 모션 제어 및 여러 로봇 간의 조정 기능을 제공하여 로봇이 창고에서 물품을 이동하도록 돕습니다. 제조 분야에서는 비전 시스템을 사용하여 정확한 핸들링을 구현하는 자동화된 피킹 및 배치 작업과 같은 고급 작업을 가능하게 합니다. 의료 분야에서는 ROS가 환자 치료를 지원하고 임상 워크플로의 효율성을 향상시키는 로봇 시스템을 지원합니다.

이름과 달리 ROS는 전통적인 의미의 운영 체제가 아니라, 개발자가 다양한 플랫폼과 프로그래밍 언어를 사용하여 로봇을 만들 수 있도록 도와주는 도구 및 라이브러리 모음입니다.

![](./assets/ROS-ecosystem.gif)

[출처 : ROS2 공식사이트](https://docs.ros.org/en/lyrical/About-ROS.html)

#### 프레임워크의 구조

ROS 프레임워크는 로봇의 통신이 가능하게 하는 기반구조로 메시징, 표준 인터페이스 외에도 다양한 기능을 포함하고 있습니다.

ROS는 다음과 같은 기본 구성 요소로 이루어져 있습니다.

* 노드
* 인터페이스(토픽, 서비스 및 액션)
* 매개변수
* 클라이언트 라이브러리

#### 도구

ROS의 도구들은 개발자들이 로봇 시스템을 구축, 테스트 및 모니터링에 도움을 줍니다.

`시각화 도구`를 사용하면 테스트 중에 로봇의 센서, 위치 및 주변 환경을 3D로 표시할 수 있고, `발사 제어 도구`를 사용하면 개발자는 실제 배포 전에 로봇의 시동 및 작동 관리 방식을 정의하고 검증할 수 있습니다. `데이터 기록 및 재생 도구`를 사용하면 로봇의 동작을 기록하여 나중에 검토 가능합니다.

#### 통합 도구

ROS는 다른 오픈 로보틱스 플랫폼과 연동하여 개발 및 배포를 더욱 쉽게 만듭니다.

* [Gazebo](https://gazebosim.org/home) : 물리 기반 시뮬레이션을 제공하므로 개발자는 실제 하드웨어를 사용하기 전에 가상 환경에서 로봇을 테스트합니다.
* [Open-RMF](https://www.open-rmf.org/) (로봇 미들웨어 프레임워크): 다양한 로봇들이 협력하고 엘리베이터, 출입문과 같은 건물 시스템과 상호 작용할 수 있도록 지원합니다.
* [ros-controls](https://control.ros.org/rolling/index.html) : ROS를 사용하여 로봇을 실시간으로 제어할 수 있도록 해줍니다.

### 튜토리얼

#### turtlesim 재시도

초보자를 위해 설계된 경량 2D 시뮬레이션 도구인 turtlesim을 사용하면 간단한 시각적 환경에서 핵심 ROS 개념을 학습합니다.

##### 터틀심 설치

```bash
$ sudo apt update
$ sudo apt install ros-lyrical-turtlesim
```

이전에 이미 설치가 되어 있습니다.

패키지 설치를 확인하려면 아래와 같이 입력합니다.

````bash
$ ros2 pkg executables turtlesim
turtlesim draw_square
turtlesim mimic
turtlesim turtle_teleop_key
turtlesim turtlesim_node
````

##### ROS 터미널 환경설정 단순화

ROS 터미널 환경 설정을 하려면 아래의 명령어를 터미널 마다 실행해야 합니다.

```bash
$ source /opt/ros/lyrical/setup.bash
```

하지만 매번 입력하기 싫으면 아래와 같이 .bashrc에 자동으로 추가합니다/

```bash
$ echo "source /opt/ros/lyrical/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
```

##### 터틀심 시작

아래의 명령어로 터틀심을 시작합니다.

```bash
$ ros2 run turtlesim turtlesim_node
[INFO] [turtlesim]: Starting turtlesim with node name /turtlesim
[INFO] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
```

![](assets/20260820_161657_image.png)

랜덤하게 바뀌는 거북이 모양의 TurtleSim 창이 열립니다.

##### 터틀심 사용

새 터미널을 열고 ROS 2를 다시 소싱합니다.

첫 번째 노드의 거북이를 제어하기 위해 새 노드를 실행합니다.

```bash
$ ros2 run turtlesim turtle_teleop_key
```

키보드의 방향키를 사용하여 거북이를 조종하세요. 거북이는 화면을 돌아다니며, 몸에 달린 "펜"으로 지금까지 이동한 경로를 그립니다.

- list

각 명령어의 하위 명령어 를 사용하면 노드와 해당 노드에 연결된 토픽, 서비스 및 액션을 확인할 수 있습니다 .

```bash
$ ros2 node list
$ ros2 topic list
$ ros2 service list
$ ros2 action list
```

터틀심에서 위 명령어의 결과는 아래와 같습니다.

```bash
hugo@hugo:~$ ros2 node list
/teleop_turtle
/turtlesim
hugo@hugo:~$ ros2 topic list
/parameter_events
/rosout
/turtle1/cmd_vel
/turtle1/color_sensor
/turtle1/pose
hugo@hugo:~$ ros2 service list
/clear
/kill
/reset
/spawn
/teleop_turtle/describe_parameters
/teleop_turtle/get_parameter_types
/teleop_turtle/get_parameters
/teleop_turtle/get_type_description
/teleop_turtle/list_parameters
/teleop_turtle/set_parameters
/teleop_turtle/set_parameters_atomically
/turtle1/set_pen
/turtle1/teleport_absolute
/turtle1/teleport_relative
/turtlesim/describe_parameters
/turtlesim/get_parameter_types
/turtlesim/get_parameters
/turtlesim/get_type_description
/turtlesim/list_parameters
/turtlesim/set_parameters
/turtlesim/set_parameters_atomically
hugo@hugo:~$ ros2 action list
/turtle1/rotate_absolute

```

##### rqt 설치

ROS2의 상태를 확인하고 제어하는 GUI 입니다.

새 터미널에서 아래의 명령을 수행합니다.

```bash
$ sudo apt update
$ sudo apt install ros-lyrical-rqt ros-lyrical-rqt-common-plugins
```

##### rqt 실행

새로운 터미널에서 아래의 명령으로 rqt를 실행합니다.

```bash
$ source /opt/ros/lyrical/setup.bash
rqt
```

생성된 rqt에서 Plugins → Services → Service Caller 를 선택하고, 생성된 화면의 Service에서 `/spawn`을 선택하고, 아래의 내용을 입력합니다.

```
x: 2.0
y: 2.0
theta: 0.0
name: turtle2
```

이제 Call 버튼을 클릭하면,

![](assets/20260821_145453_image.png)

아래와 같이 turtlesim 창에 새로운 두번째 거북이가 생성됩니다.

![](assets/20260821_145519_image.png)

##### 거북이 삭제

Service에서 /kill 을 선택합니다. Topic 아래의 name에 'turtle2' 를 입력하고 Call을 클릭하면 새롭게 만들어졌던 두번째 거북이가 사라집니다.

##### 거북이 제어

토픽으로 거북이를 움직일 수는 없습니다.

```bash
$ ros2 run turtlesim turtle_teleop_key
```

이전에 확인했던 명령어로 키보드 움직임이 가능하고, 아래의 명령어로 직접 배포하여 동작시킬 수 있습니다.

```bash
$ ros2 topic pub --once /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 1.0}}"
publisher: beginning loop
publishing #1: geometry_msgs.msg.Twist(linear=geometry_msgs.msg.Vector3(x=2.0, y=0.0, z=0.0), angular=geometry_msgs.msg.Vector3(x=0.0, y=0.0, z=1.0))

```

![](assets/20260821_150511_image.png)

또는, 아래와 같이 명령어를 입력하고 실행하면,

```bash
$ ros2 topic pub --rate 10 /turtle1/cmd_vel geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 1.0}}"

```

![](assets/20260821_150947_image.png)



계속 원을 그리며 움직입니다.
