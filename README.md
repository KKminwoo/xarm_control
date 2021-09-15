## 1. UFACTORY 사이트

[UFACTORY Official Website](https://www.ufactory.cc/)

- 소프트웨어 다운로드

[Download-xArm](https://www.ufactory.cc/pages/download-xarm)

- ros

[xArm-Developer/xarm_ros](https://github.com/xArm-Developer/xarm_ros?v=1597982270402)

- xArm-Python-SDK

[xArm-Developer/xArm-Python-SDK](https://github.com/xArm-Developer/xArm-Python-SDK?v=1597982270402)

## 2. 메뉴얼

- 사용자 메뉴얼

    [xArm_User_Manual-1.6.0.pdf](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8f07be99-c169-456d-931f-2d536485fe3d/xArm_User_Manual-1.6.0.pdf)

    61페이지 로봇 연결방법 설명

- 개발자 메뉴얼

    [xArm_Developer_Manual-1.6.0.pdf](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4b419a63-6e76-463a-b748-9286d254bca3/xArm_Developer_Manual-1.6.0.pdf)

### 초기 setting

- 컴퓨터 이더넷 네트워크(ip 주소를 192.168.1.208과 다르게 해줘야 함)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de44a21b-ce41-4fd3-9ae2-4af76ac77007/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de44a21b-ce41-4fd3-9ae2-4af76ac77007/Untitled.png)

### moveit! 동작 확인

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e25f6e4d-189d-4c0b-869b-35382a54c3b3/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e25f6e4d-189d-4c0b-869b-35382a54c3b3/Untitled.png)

### launch 실행

```bash
# xarm rviz 실행
roslaunch xarm6_moveit_config realMove_exec.launch

# rgbd camera 실행: 카메라 키는 파일
roslaunch realsense2_camera rs_rgbd.launch initial_reset:=true

# find object 2d 실행: 카메라를 통해서 물체 사진 불러오는 파일 -> feature 추출을 하려고 했으나 추후에 marker로 변경
roslaunch find_object_2d find_object_3d.launch

# fiducials detection 실행
roslaunch aruco_detect aruco_detect.launch
```

---

### (중요!!) static_transform_publisher

- demo.launch파일 수정
- static_transform_publisher x y z yaw pitch roll frame_id child_frame_id period_in_ms
Publish a static coordinate transform to tf using an x/y/z offset in meters and yaw/pitch/roll in radians. (yaw is rotation about Z, pitch is rotation about Y, and roll is rotation about X). The period, in milliseconds, specifies how often to send a transform. 100ms (10hz) is a good value.

```xml
<!-- 링크 8 뒹 camera_link라는 프레임 생성 -->
 <launch>
   2 <node pkg="tf" type="static_transform_publisher" name="link1_broadcaster" args="1 0 0 0 0 0 1 link1_parent link1 100" />
   3 </launch>

<node pkg="tf" type="static_transform_publisher" name="_t" args="1 0 0 0 0 1 panda_link8 camera_link 100" />
```
