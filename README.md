# Intelproject5
인텔프로젝트5팀

## 👥 팀 구성 및 역할

| 이름     | 담당 역할 |
|----------|-----------|
| **김민우**   | 점수 계산 로직, JETSON NANO 구동 |
| **김재용**   | 헤일로 보드 구동, UI/UX |
| **민주영**   | 캐릭터 파츠 리깅, 캐릭터 렌더링 |
| **황정태**   | 카메라 팬틸트, UI/UX |
| **박진수**   | 점수 계산 로직, UI/UX |
| **이진이**   | 캐릭터 모듈링, 캐릭터 렌더링 |

---

## 🗓️ 프로젝트 일정

| 날짜 범위     | 주요 작업 |
|---------------|-----------|
| `9.1 ~ 9.2`     | 기획 |
| `9.3 ~ 9.4`     | UI 기획 |
| `9.5`           | 캐릭터 컨셉 |
| `9.6 ~ 9.7`     | 캐릭터 보드 |
| `9.9 ~ 9.10`    | 캐릭터 모션 |
| `9.11 ~ 9.12`   | 캐릭터 모션 |
| `9.13 ~ 9.14`   | 캐릭터 모션 |
| `9.15 ~ 9.16`   | 캐릭터 모션 |
| `9.17 ~ 9.18`   | PPT 작성 및 발표 준비 |


---

# Street_Reels_Fighter

## 프로젝트 목표
릴스에서 유행하는 춤을 Pose Estimation을 통해 연습 및 대결할 수 있게 하는 기능을 제공하는 게임 시스템입니다.

### 주요 기능
- YOLOv8-Pose로 User / Reference video에서 Keypoint 추출
- 추출한 Key Point로 관절 각도를 계산하여 유사도 / 점수 측정
- Key Point - 아바타 파츠 매핑으로 아바타 영상 생성
- STM32 + UART로 서보 모터 Pan (좌/중/우 추적)
- 듀얼 모니터 : Control(조작) / View(무대) 분리


### 트러블 슈팅
1. Touch Display 터치 좌표 오류
    - 문제 : Touch Display와 일반 Display를 동시 사용했을 때 터치 디스플레이에 터치되는 좌표 값이 정확하지 않음
    - 원인 : 어떤 것이 Touch Display인지 알지 못하고 하나의 좌표 값으로 인식했기 때문
    - 해결 : Xorg 기준으로 Touch Display를 특정 모니터에 매핑하여 정확한 좌표를 사용
    - 명령 : xinput map-to-output <터치장치ID> <모니터이름> : ex) xinput map-to-output 12 HDMI-1

2. 실행할 카메라 번호 오류
    - 문제 : 카메라 케이블 재연결 후 프로그램 실행 시 입력 장치를 못 찾음
    - 원인 : /dev/video0가 /dev/video1 등으로 장치 번호가 바뀜
    - 해결 : 카메라 파일 번호 변경



## 시연 영상
(시연 영상 1)

https://github.com/user-attachments/assets/3b85f136-1a0b-4b7d-9cec-c0dcfc4e700a

(시연 영상 2)

https://github.com/user-attachments/assets/82aec550-789e-4134-bfa7-d9a611d72db9

(View 모니터 영상)

https://github.com/user-attachments/assets/fc612eb9-a9f8-4c21-be08-f8b29d156aaa

(Control 모니터 영상)

https://github.com/user-attachments/assets/b6bfb8c5-b38f-4104-90f9-4563830ba4b2





## 구성도
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/10bc5493-2cbd-427e-8ccc-1254b1499612" />




## 흐름도
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/88f75fc4-9132-4528-b9f9-8a906baca271" />



## 팀 역할
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/43a84000-a948-4d23-b2fc-cde58099058e" />



### Key Point 추출
<img width="878" height="936" alt="image" src="https://github.com/user-attachments/assets/ea55223d-63bd-49b0-9c76-c5e92dbff430" />


### 관절 각도 계산
<img width="1431" height="926" alt="image" src="https://github.com/user-attachments/assets/f5e19040-a71d-4c29-85e4-006b205297dc" />


### 아바타 생성
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/8aa3ff1c-1142-47d3-ad26-6116e9ac6e31" />


### 카메라 Pan (STM32)
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/b994d77f-d89b-4535-a556-3a9f32b39cfb" />
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/5e236b3a-aa04-439d-9fdc-c2151ecf3bc1" />




## 전체 자료
[스릴파_뚝's딱's_상세 발표 자료.pdf](https://github.com/user-attachments/files/22405165/_.s.s_.pdf)
