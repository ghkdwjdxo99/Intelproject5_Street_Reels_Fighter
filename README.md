# Street_Reels_Fighter
- 인텔 프로젝트 5팀
- Street_Reels_Fighter는 릴스에서 유행하는 춤을 Pose Estimation과 아바타 렌더링으로 연습하고 대결할 수 있는 듀얼 모니터 기반 리듬 게임입니다.
- 모니터 1 + 터치 디스플레이, STM32를 연동해 구현했습니다.
- 최종 동작 버전 코드는 `gui/SRF_v2.0.6` 디렉터리에 정리되어 있습니다.

## 프로젝트 요약
- YOLOv8 Pose로 사용자와 레퍼런스 영상의 Keypoint를 추출하고, 관절 각도 기반 점수화 로직 구현
- 추출한 Key Point는 아바타 파츠에 매핑되어 다양한 캐릭터 영상으로 변환
- 듀얼 모니터 구성으로 `Control(터치 패널)`과 `View(무대 연출)`를 분리하여 사용자가 곡 선택과 세션 관리를 수행
- STM32 + UART로 Pan 서보 모터를 제어하여 플레이어를 화면 중앙에 유지

## 주요 기능
- YOLOv8-Pose 기반 사용자/레퍼런스 Keypoint 추출 및 JSON 변환 (`merge_test/video_to_json.py`)
- 관절 각도, 구간별 가중치, 정상화 로직으로 점수 산출 (`merge_test/pages/pose_score_app.py`)
- QML + PyQt5 UI로 싱글/멀티 플레이, 곡 선택, 아바타 변환, 결과 화면 제공
- STM32/터치 디스플레이와의 연동: 카메라 추적, UI 조작, 점수 피드백 애니메이션

## 시스템 구성
- **소프트웨어**
  - Python + PyQt5 QML 런타임 (`gui/SRF_v2.0.6/main.py`)
  - YOLOv8 Pose 모델(`merge_test/yolov8l-pose.pt`)과 Ultralytics 프레임워크
  - OpenCV 기반 영상 입출력, Numpy 연산, PySerial을 통한 장치 통신
- **하드웨어**
  - STM32 보드 (Pan/Tilt 서보 모터 제어 및 상태 동기화)
  - 듀얼 모니터(터치 패널 + 무대 화면), USB 카메라

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

## 디렉터리 가이드
- `gui/SRF_v2.0.6/` : 최종 빌드용 PyQt5/QML 애플리케이션.
- `gui/SRF_v2.0.6/resource/` : UI 영상, 이미지, 폰트, 샘플 레퍼런스 데이터.
- `gui/SRF_v2.0.6/merge_test/` : 포즈 추론, 점수 계산, 아바타 렌더링 백엔드 로직.
- `avatar/` : 캐릭터 에셋 및 리깅 자료.
- `model/` : 머신러닝 모델 관련 부가 자료.
- `stm32/` : 서보 제어용 펌웨어 및 회로 문서.

## 트러블 슈팅
1. **터치 디스플레이 좌표값 오류**
   - 원인: Xorg에서 터치 장치를 특정 모니터와 매핑하지 않아 좌표가 틀어짐.
   - 해결: `xinput map-to-output <터치장치ID> <모니터이름>` 명령으로 터치 입력을 해당 디스플레이에 매핑.
2. **카메라 장치 번호 변동**
   - 원인: USB 재연결 시 `/dev/video0` → `/dev/video1` 등으로 번호가 변경됨.
   - 해결: 실행 전에 `v4l2-ctl --list-devices`로 장치 번호 확인 후 설정값 반영.



## 시연 영상
(시연 영상 1)

https://github.com/user-attachments/assets/3b85f136-1a0b-4b7d-9cec-c0dcfc4e700a

(시연 영상 2)

https://github.com/user-attachments/assets/82aec550-789e-4134-bfa7-d9a611d72db9

(View 모니터 영상)

https://github.com/user-attachments/assets/fc612eb9-a9f8-4c21-be08-f8b29d156aaa

(Control 모니터 영상)

https://github.com/user-attachments/assets/b6bfb8c5-b38f-4104-90f9-4563830ba4b2





### 구성도
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/10bc5493-2cbd-427e-8ccc-1254b1499612" />




### 흐름도
<img width="2560" height="1440" alt="image" src="https://github.com/user-attachments/assets/88f75fc4-9132-4528-b9f9-8a906baca271" />



### 팀 역할
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
