# 2021-Object-Detection-Yonsei-AI-Challenge
# 2021 Ai Challenge
팀명: 천재지변 김성준
팀장: 전용준
팀원: 공다흰 김성준
주제: 캠퍼스 내 건물 인식 후 건물 설명 팝업창 띄우기

#목차
1. Labeling
2. Training 방법
3. Detect 방법
4. 휴대폰을 웹캠으로 사용하는 방법
5. 팝업창 띄우기 

# 실험환경
Macbook Air m1 

#Data Set
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

# Labeling
1. https://github.com/tzutalin/labelImg 이동
2. <img width="60%" src="https://user-images.githubusercontent.com/78187434/147383069-5c09d376-bde0-4ba7-9698-449965761074.png"/>
3. <img width="60%" src="https://user-images.githubusercontent.com/78187434/147383111-a52c02d5-b613-4183-b7a5-f2be0abe6421.png"/>
4. <img width="60%" src="https://user-images.githubusercontent.com/78187434/147383122-ff4ebb7a-0a3c-4062-8e68-89a36d2676aa.png"/>
5. 본인의 데이터셋의 Label입력
 <img width="70%" src="https://user-images.githubusercontent.com/78187434/147383142-a0b69eb8-aeb6-43f4-8c94-a86b116dba16.png"/>
6. <img width="70%" src="https://user-images.githubusercontent.com/78187434/147383161-d5c10998-0e29-4e63-9346-b0ffa385e82d.png"/>
7. <img width="70%" src="https://user-images.githubusercontent.com/78187434/147383170-cbda3742-124b-4258-8a5c-62c20ee4051b.png"/>
8. 데이터 위치와 저장경로를 변경함 (같은 위치에 하는것이 좋음)
<img width="80%" src="https://user-images.githubusercontent.com/78187434/147383186-dabc202f-a352-41bc-8ee7-7cd48a02e711.png"/>

# Training
1. cfg 파일을 메모장으로 열기
2. yolo검색 후 classes 개수만큼 값을 변경
<img width="20%" src="https://user-images.githubusercontent.com/78187434/147383298-c7a2e47e-41d6-4d3c-a7b9-71751f5d8880.png"/>
3. yolo 바로 위 convolution에서 filter값을 (클래스 개수 + 5) * 3 로 수정
<img width="20%" src="https://user-images.githubusercontent.com/78187434/147383333-df26dad4-15f1-41c4-bb20-ddd3902b312b.png"/>
4. max_batches 값을 클래스 개수 * 2000 로 수정
<img width="20%" src="https://user-images.githubusercontent.com/78187434/147383406-d23ae286-daba-46b4-ba10-e7cea475dc05.png"/>
5. steps 값을 max_batches값의 80%,90% 로 수정
<img width="20%" src="https://user-images.githubusercontent.com/78187434/147383445-ca660968-c618-4087-b0ed-42359a2790ac.png"/>

