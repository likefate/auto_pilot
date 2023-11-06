# auto_pilot
# 2장 Jetpack & ROS install

이미지 : https://drive.google.com/file/d/1HU5F1cwiw2wzuNBdLL9R3Wvpg5AXLzw5/view?usp=sharing

쿨링 팬
~~~shell
cd Downloads
git clone https://github.com/jetsonworld/jetson-fan-ctl.git
cd jetson-fan-ctl

sudo sh install.sh
~~~

"sudo sh install.sh"는 리눅스 또는 UNIX 기반 시스템에서 사용되는 명령어입니다. 이 명령어는 루트 권한으로 스크립트 파일 "install.sh"를 실행하도록 하는 것을 나타냅니다. "sudo"는 슈퍼 유저(루트) 권한으로 명령을 실행하는데 사용되며, "sh"는 스크립트 인터프리터를 나타내고 "install.sh"는 실행하려는 스크립트 파일의 이름입니다. 이 명령은 시스템에 어떤 소프트웨어나 설정을 설치하거나 변경하기 위해 사용될 수 있습니다.

ROS Melodic 설치

~~~shell
cd ~/Downloads/
sudo apt update

git clone https://github.com/zeta0707/installROS.git
cd installROS
./install-ros.sh
~~~

.bashrc 수정

~~~shell
$ gedit ~/.bashrc 
# 또는 편리한 에디터로 .bashrc 열기

# 파일 제일 아래에 다음과 같은 내용 입력
alias cma='catkin_make -DCATKIN_WHITELIST_PACKAGES=""'
alias cop='catkin_make --only-pkg-with-deps'
alias sds='source devel/setup.bash'
alias coc='catkin clean'
alias cca='catkin clean -y'

# mirco USB 케이블 연결을 사용할 경우, jetson master
export ROS_MASTER_URI=http://192.168.55.1:11311
export ROS_IP=192.168.55.1

source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bas

# 에디터 종료 후 터미널 업데이트
$ source ~/.bashrc
~~~

alias란? 별칭을 의미함. 긴 코드를 예악어로서 실행되도록 해준다.

catkin workspace 설치

~~~shell
jetson@jp4512G:~/catkin_ws$ cca
jetson@jp4512G:~/catkin_ws$ cma
~~~

# 3장

Jessicar install

~~~shell
cd ~/catkin_ws/src
git clone https://github.com/zeta0707/jessicar.git
cd ~/catkin_ws

cma
~~~

ROS Package 설치

~~~shell
$ sudo apt update
$ sudo apt install ros-melodic-joy* \
ros-melodic-teleop-twist-joy ros-melodic-teleop-twist-keyboard \
python-smbus ros-melodic-ackermann-msgs ros-melodic-web-video-server \
ros-melodic-image-pipeline python-pip

$ pip2 install Adafruit_PCA9685
~~~

# 5장

teleop_keyboard 키 사용 방법

~~~shell
Control Your Robot!
---------------------------
Moving around:
        w
   a    s    d
        x

w/x : increase/decrease linear velocity (~ 1.2 m/s)
a/d : increase/decrease angular velocity (~ 1.8)

space key, s : force stop

CTRL-C to quit
~~~

실행

~~~shell
# terminal #1
$ roslaunch jessicar_control keyboard_control.launch

# terminal #2
$ roslaunch jessicar_teleop jessicar_teleop_key.launch
~~~

# 6장

CSI 카메라 확인

~~~shell
$ sudo apt install ros-melodic-image-view
~~~

~~~shell
# terminal #1
$ roslaunch jessicar_camera csicam.launch
# terminal #2, PC or Jetson
$ rqt_image_view
~~~

# 7장

Blob Tracking

~~~shell
# terminal #1
$ roslaunch jessicar_control blob_all.launch

# image_view 실행, 이미지를 확인하기 위함, DISPLAY 필요
$ rosrun image_view image_view image:=/blob/image_blob
~~~

기본은 초록색으로 설정되어 있음.

~~~shell
#물체를 인식하면 다음 로그가 보일 것입니다.
[INFO] [1689681880.624880]: is_detected, Steering = -0.0 Throttle = 0.2
[INFO] [1689681880.811534]: BlobX -0.02
[INFO] [1689681880.821137]: is_detected, Steering = -0.0 Throttle = 0.2
[INFO] [1689681881.011281]: BlobX -0.02
[INFO] [1689681881.020758]: is_detected, Steering = -0.0 Throttle = 0.2
[INFO] [1689681881.211245]: BlobX -0.02
[INFO] [1689681881.217109]: is_detected, Steering = -0.0 Throttle = 0.2
~~~
