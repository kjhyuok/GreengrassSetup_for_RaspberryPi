# GreengrassSetup_for_RaspberryPi
This configuration helps you use AWS Greengrass using Raspberry Pi devices.

AWS IoT Greengrass extends AWS to edge devices so that they can act on the data they generate, while they use the AWS Cloud for management, analytics, and durable storage. Install the AWS IoT Greengrass Core software on edge devices to integrate with AWS IoT Greengrass and the AWS Cloud.

이 페이지에서는 GG를 Raspberry Pi에 설치할 수 있는 환경설정을 기록 합니다.

1. 실습 준비
**Raspberry Pi 환경 준비**

   **Raspberry Pi를 디바이스로 활용**

본 실습은 Raspberry **Pi OS를 탑재한 —Raspberry Pi 4 Computer— 디바이스를 사용하여 진행하며, 다음의 준비가 필요 합니다.
장치 준비: 라즈베리파이 본체, sd카드, sd카드 리더기, Micro HDMI Cable, 모니터, 키보드, 마우스, USB C Type 전원 Cable
하단 사진과 같은 라즈베리파이, sd카드, sd카드 리더기 확인**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bfb0f10a-d9d5-4a35-ae99-29a39d292f49/Untitled.png)

1. OS 설치 작업

필요한 장치가 모두 준비되었다면,
준비된 디바이스에 맞는 OS설치를 위해 먼저 [**Raspberry Pi OS]**([https://www.raspberrypi.com/software/](https://www.raspberrypi.com/software/))로 이동합니다.
자신의 랩탑에 맞는 OS Installer를 선택 후 설치합니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/87d54212-f527-492f-a074-2810353a57d6/Untitled.png)

정상적으로 설치를 마치고 실행한다면, 아래와 같은 스크린샷과 같은 **Raspberry Pi Imager 프로그램이 구동 됩니다. (Mac OS기준)**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/612db139-754c-46d1-a380-0ebb0d201142/Untitled.png)

OS 설치를 위해 다음과 같이 진행합니다.
운영체제 > Other general-purpose OS > Ubuntu Desktop 22.04.1 LTS(2022/09/25기준)

[화면 기록 2022-09-24 오후 9.36.50.mov](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aeb833b1-bf7c-4560-b797-de14fd5a57e0/%E1%84%92%E1%85%AA%E1%84%86%E1%85%A7%E1%86%AB_%E1%84%80%E1%85%B5%E1%84%85%E1%85%A9%E1%86%A8_2022-09-24_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.36.50.mov)

다음은 *저장소(외장 MicroSD Card)*를 선택 하고 *쓰기* 버튼을 클릭 합니다.

- 꼭 MicroSD Card 가 맞는지 확인해 주세요.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17655464-df14-4f20-ba3d-ef243b048490/Untitled.png)

- 쓰기가 완료되면 확인 단계로 넘어가며 progress bar가 100% 될 때 까지 SD Card를 제거하지 말고 대기 합니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1633cd41-c275-4e16-84b3-f8f8f215ca70/Untitled.png)

OS 쓰기작업에 대한 확인이 완료 되면 아래와 같은 완료 메시지를 확인하고 SD Card를 랩탑에서 제거 합니다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e0a98d2-c3e8-44ff-a5ee-82938a90dda5/Untitled.png)

1. **Raspberry Pi 에 Ubuntu OS환경설정**
- SD Card를 사진과 같이 **Raspberry Pi 디바이스 뒷면에 삽입합니다.(삽입 방향을 유의해주세요.)**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4974c574-4da2-4662-a235-5212f16fa703/Untitled.png)

- 준비된 입력/출력 장치를 모두 연결합니다. (키보드, 마우스, 모니터와 **Micro HDMI Cable 등)**
- 마지막으로 **USB C Type 전원 Cable을 연결하여 Raspberry Pi 디바이스에 전원을 인가 합니다.**
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/19207b03-3398-4c11-abed-c11cf1541d51/Untitled.png)

- 모든 장치와 연결 후 Ubuntu OS의 초기 설정을 진행 합니다.
- Ubuntu OS 계정설정을 완료 후 다음과 같이 Terminal을 열고 설치한 OS와 SD card를 체크합니다.
- OS version: cat /etc/issue
- Disk: df -h
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b17788d9-58e6-4be0-afa1-e0fe7a00b483/Untitled.png)
    

//ssh 설정

# 관련 프로그램 설치
sudo apt-get install -y openssh-server 

# 시스템 재시작
sudo systemctl restart ssh

# 시스템 가동
sudo systemctl enable ssh

#방화벽 허용

sudo ufw allow 22

#설정 IP 확인

sudo apt install -y net-tools

ifconfig

==============생략

**AWS IoT Greengrass 실습을 위한 Linux 환경 체크
0.** sudo apt update
1. `sudo apt-get install openjdk-8-jdk`
2.`sudo apt-get install libglib2.0-dev`
3.`sudo apt install python3.8`
4. `sudo snap install curl`
5# install awscli
`$ **curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip"**`

unzip awscliv2.zip
sudo ./aws/install

1. sudo apt install -y python3-pip (greengrass deployment 과정에 필요함)
2. sudo apt install -y git (5. ML 추론 과정)

축하합니다. **Raspberry Pi 디바이스로 AWS IoT Greengrass를 실습할 준비가 완료 되었습니다.**

중요: 이 후의 실습 과정에 포함된 Linux Command 가 포함된 스크린샷은 AWS Cloud 9(Ubuntu OS)환경 기준으로 준비되어 있습니다. 
         현재 설정한 **Raspberry Pi와 같으므로** 수행해야 할 Linux Command 는 동일하게 실습에 참고하시면 됩니다.

============= 코멘트

---

## **Error**

1) 

**현상** : ‘5. 디바이스에서 ML 추론 - ML Greengrass 컴포넌트 배포’에서 imageclassification component 배포 실패

**로그** : 

- tail -f /greengrass/v2/logs/greengrass.log

[ERROR] (pool-2-thread-26) com.aws.greengrass.componentmanager.ComponentManager: Failed to prepare package com.example.ImgClassification-v1.0.0. {}
com.aws.greengrass.componentmanager.exceptions.PackageDownloadException: Failed to change permissions of component com.example.ImgClassification-v1.0.0 artifact ComponentArtifact(artifactUri=s3://mybucket-678089554237/ggv2/artifacts/my-model.zip, checksum=22aToiE/RGGyxarKV67hQU8AMR6v5Oi5SRA75WJ8MjE=, algorithm=SHA-256, unarchive=ZIP, permission=Permission(read=OWNER, execute=NONE))

해결 :

- deployment 실패한 상태에서 2번째 시도하면 permission 에러가 난다..
- component 삭제, s3 mybucket-<계정>안에 artifact 삭제, /greengrass/v2/packages 안에 있는 imgClassfication 폴더들 삭제 후 create_gg_component 다시 하면 됨
- 

2)

현상 : ‘5. 디바이스에서 ML 추론 - ML Greengrass 컴포넌트 배포’에서 imageclassification component 배포 실패

로그 : 

- tail -f /greengrass/v2/logs/greengrass.log

2022-09-27T14:22:57.070Z [WARN] (Copier) com.example.ImgClassification: stderr. /greengrass/v2/packages/artifacts-unarchived/com.example.ImgClassification/1.0.0/my-model/run.sh: line 6: gcv/bin/activate: No such file or directory. {scriptName=services.com.example.ImgClassification.lifecycle.Run.script, serviceName=com.example.ImgClassification, currentState=RUNNING}

해결:

- $ sudo apt install -y python3.8-dev python3.8-venv

3)

현상: 

로그:

[imgClassificationErr.rtf](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc8ae9f1-bdbc-4d69-a826-84b4904cd4b4/imgClassificationErr.rtf)

해결

- XX..
- $ file /greengrass/v2/packages/artifacts-unarchived/com.example.ImgClassification/1.0.0/my-model/model_cpu/libdlr.so: ELF 64-bit LSB shared object, x86-64, version 1 (GNU/Linux)  ⇒ x86 라이브러리라서 load 되지 않는 것 같음
- **ggv2-deploy-on-device에 있는 스크립트를 실행해서 component생성해야 함**

4)

로그 : ERROR: opencv_python-4.5.3+c1cc7e5-cp36-cp36m-linux_aarch64.whl

해결 : [install.sh](http://install.sh) 수정해줘야함, [https://github.com/neo-ai/neo-ai-dlr/releases](https://github.com/neo-ai/neo-ai-dlr/releases) 여기서 rasp4b용써야함..

5)

로그 : stderr. ImportError: OpenCV loader: missing configuration file: ['[config-3.8.py](http://config-3.8.py/)', '[config-3.py](http://config-3.py/)']. Check OpenCV installation.. {scriptName=services.com.bioplus.ImgClassification.lifecycle.Run.script, serviceName=com.bioplus.ImgClassification, currentState=RUNNING}

해결 : pyinstaller --onefile --paths="/usr/lib/python3.9/site-packages/cv2/python-3.9" [main.py](http://main.py/)

`pip install pyinstaller`

([https://github.com/opencv/opencv/issues/14064](https://github.com/opencv/opencv/issues/14064))

`pip install opencv-python`

[https://github.com/daekeun-ml/aiot-e2e-sagemaker-greengrass-v2-nvidia-jetson/tree/main/ggv2-deploy-on-device](https://github.com/daekeun-ml/aiot-e2e-sagemaker-greengrass-v2-nvidia-jetson/tree/main/ggv2-deploy-on-device)

---

## TroubleShooting

Err : **[python-dev installation error: ImportError: No module named apt_pkg](https://stackoverflow.com/questions/13708180/python-dev-installation-error-importerror-no-module-named-apt-pkg)**

Sol : 

```powershell
$ cd /usr/lib/python3/dist-packages/
$ sudo ln -s apt_pkg.cpython-36m-x86_64-linux-gnu.so apt_pkg.so
```
