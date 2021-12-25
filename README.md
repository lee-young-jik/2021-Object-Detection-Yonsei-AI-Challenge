# 2021-Object-Detection-Yonsei-AI-Challenge
팀명: 천재지변 김성준
<br>
팀장: 전용준 <br>
팀원: 공다흰 김성준 <br>
주제: 캠퍼스 내 건물 인식 후 건물 설명 팝업창 띄우기
### Supervised and helped by C-J Lee, S-R Hwang, and H-U Yoon
## 목차
1. Labeling
2. Training 방법
3. Detect 방법
4. 팝업창 띄우기 
5. Reference

## 실행 환경
- Macbook Air m1 
- opencv

## Challenge
웹캠을 이용한 실시간 건물 탐지

## Data Set
- 스포츠센터
- 연세 플라자
- 대학 본부
- 학관
- 청송관
- 정의관
- 창조관
- 미래관
- 도서관 
- 백운관

## Labeling
1. https://github.com/tzutalin/labelImg 이동
2. <img width="60%" src="https://user-images.githubusercontent.com/78187434/147383069-5c09d376-bde0-4ba7-9698-449965761074.png"/>
3. <img width="60%" src="https://user-images.githubusercontent.com/78187434/147383111-a52c02d5-b613-4183-b7a5-f2be0abe6421.png"/>
4. <img width="60%" src="https://user-images.githubusercontent.com/78187434/147383122-ff4ebb7a-0a3c-4062-8e68-89a36d2676aa.png"/>
5. 본인의 데이터셋의 Label입력
 <img width="30%" src="https://user-images.githubusercontent.com/78187434/147383142-a0b69eb8-aeb6-43f4-8c94-a86b116dba16.png"/>
6. <img width="70%" src="https://user-images.githubusercontent.com/78187434/147383161-d5c10998-0e29-4e63-9346-b0ffa385e82d.png"/>
7. <img width="70%" src="https://user-images.githubusercontent.com/78187434/147383170-cbda3742-124b-4258-8a5c-62c20ee4051b.png"/>
8. 데이터 위치와 저장경로를 변경함 (같은 위치에 하는것이 좋음)
<img width="80%" src="https://user-images.githubusercontent.com/78187434/147383186-dabc202f-a352-41bc-8ee7-7cd48a02e711.png"/>

## Training Setup
1. cfg 파일을 메모장으로 열기

2. yolo검색 후 classes 개수만큼 값을 변경
<img width="50%" src="https://user-images.githubusercontent.com/78187434/147383298-c7a2e47e-41d6-4d3c-a7b9-71751f5d8880.png"/>

3. yolo 바로 위 convolution에서 filter값을 (클래스 개수 + 5) * 3 로 수정
<img width="50%" src="https://user-images.githubusercontent.com/78187434/147383333-df26dad4-15f1-41c4-bb20-ddd3902b312b.png"/>

4. max_batches 값을 클래스 개수 * 2000 로 수정
<img width="20%" src="https://user-images.githubusercontent.com/78187434/147383406-d23ae286-daba-46b4-ba10-e7cea475dc05.png"/>

5. steps 값을 max_batches값의 80%,90% 로 수정
<img width="20%" src="https://user-images.githubusercontent.com/78187434/147383445-ca660968-c618-4087-b0ed-42359a2790ac.png"/>

6. obj.names 파일 수정 ==> labeling class 순서대로 작성
<img width="40%" src="https://user-images.githubusercontent.com/78187434/147383975-1b94f507-1f46-4725-a474-8af194fed3e6.png"/>

7. obj.data 파일 수정 ==> 클래스 개수와, train, valid txt파일의 위치 수정 
<img width="40%" src="https://user-images.githubusercontent.com/78187434/147384071-18e8bdb3-0ac4-4bf1-a0ca-1c3fbeadccaa.png"/>

8. Weight File 다운로드 ==> tiny wolo weight 파일 다운로드 후 폴더에다가 넣어줌
https://pjreddie.com/darknet/yolo/https://pjreddie.com/darknet/yolo/
<img width="60%" src="https://user-images.githubusercontent.com/78187434/147385425-47d1fc9a-8230-4cb7-b975-7d75f625ed28.png"/>

## Training
1. 트레이닝 시작<br>
생성한 obj파일, cfg파일, weight파일을 이용해서 training 시작<br>
./darknet detector train data/obj.data yolo-obj.cfg yolov4.conv.137 <br>
본인이 저장해 놓은 obj.data, cfg파일, weight파일 경로로 수정해서 명령어 실행<br>

2. 전이학습 <br>
./darknet detector train data/obj.data cfg/custom-yolov4-detector.cfg /content/darknet/backup/custom-yolov4-detector_last.weights<br>
이전에 학습해놓은 weight파일을 이용해서 연속적으로 학습을 진행<br>

## Detect
### weight 파일 다운로드 (Yonsei 계정으로 접속해야 다운로드 가능합니다)<br>
https://drive.google.com/file/d/1UlTw_5hbfAx5hHGg5MehXO8ZcqVD2JLb/view?usp=sharing

# 동영상 탐지 <br>
./darknet detector demo cfg/obj.data cfg/custom-yolov4-detector.cfg cfg/custom-yolov4-detector_90_weight_file.weights data/video/library.mp4<br>
# 본인의 obj.data cfg weight 탐지할 데이터 파일의 경로로 수정해서 사용<br>

# 이미지 탐지<br>
./darknet detector test cfg/augmentation/obj.data cfg/augmentation/custom-yolov4-detector.cfg cfg/augmentation/custom-yolov4-detector_last.weights data/채/academy.jpg<br>

# 웹캠 이용<br>
darknet detector demo cfg/augmentation/obj.data cfg/augmentation/custom-yolov4-detector.cfg cfg/augmentation/custom-yolov4-detector_last.weights -c 0<br>

## 팝업창 코드 설명<br>
1.image_opencv.cpp파일 <br>
extern "C" void draw_detections_cv_v3(mat_cv* mat, detection *dets, int num, float thresh, char **names, image **alphabet, int classes, int ext_output) 함수를 수정함<br>
<img width="70%" src="https://user-images.githubusercontent.com/78187434/147386425-b38d08d1-5380-498e-a5ff-be788930a7b7.png"/><br>
탐지한 클래스가 80% 이상일 경우 해당 건물에 대한 팝업창을 출력<br>

# 만약에 이미지에 대한 팝업창을 띄우고 싶다면 image.c 파일을 수정해주면 된다. ==> 수정 후 다시 디버깅<br>

## 결과 
<img width="60%" src="https://user-images.githubusercontent.com/78187434/147386610-78d8aea0-7dc7-4d44-b8b9-5a30192c6179.png"/>

# 새로운 건물 데이터에 대해서 90% 이상의 정확도를 보여준다

## Reference
https://github.com/AlexeyAB/darknet#custom-object-detection <br>
https://deep-eye.tistory.com/53
