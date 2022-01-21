- Box를 검출하는 알고리즘 
1. Box를 bounding box를 통해 검출한다.
2. Box를 segmentation을 통해 검출한다


## Purpose
- Yolo 구현을 목표로 하여 custom dataset인 box에 적용해본다 -> center 파지점도 검출.
- 먼저 이런 멋진 [Tutorial](https://blog.paperspace.com/how-to-implement-a-yolo-object-detector-in-pytorch/) 의 존재에 감사하며 이걸 먼저 따라 해보기로 함. [Full code](https://github.com/ayooshkathuria/YOLO_v3_tutorial_from_scratch)
- 한국어 번역 version [here](https://deep-learning-study.tistory.com/411)
- 구성은 다음과 같음 
1. [Understanding How YOLO works](https://github.com/ChaeChae0505/Pytorch/blob/main/Miniproject/220120/1.UnderstandYOLO.md)
2. Creating the layers of the network architecture
3. Implementing the the forward pass of the network
4. Objectness score thresholding and Non-maximum suppression
5. Designing the input and the output pipelines
- 이외에 custom dataset 사용을 위해 추가로 Data 포맷 및 load 방법을 알아볼 것이다

---
## 헷갈리는 부분들 
- loss function 으로 bounding box regression을 한다고 하는데,,,, 어떻게 하는 것이지...? 목적 함수가 어떻게 돌아가는지 이해가 되지 않는다.
- 객체의 localization은 도대체 어떻게 하는 것인가?
- **이 부분을 알아야하는 이유 : 나는 rotation도 한꺼번에 예측하는 모델을 만들고 싶다 제발**

### Object detection (DIoU, CIoU)
- localization을 위한 bounding box regression은 l1, l2 norm 의 목적 함수로 훈련되는 것이 일반적이다. ( 그렇다면 입력할 때 ground truth를 5개 주면 5개 예측할 수 있겠네?) 
- bounding box regression 성능 평가는 l1, L2 norm의 스케일과 해석의 비직관성으로 인해 타겟 박스와 (라벨) 예측한 박스가 겹치는 정도를 나타낸 IoU를 (Intersection over Union) 사용합니다 
- 테스트 메트릭과(IoU) 목적함수의 (L1, L2) 불일치를 극복하기 위해 IoU 자체를 목적함수로 하는 방법들이 여럿 제안 되었다고 한다,,,,,,(ex) Liou = 1- IoU )
- 이를 개선하기 위해 제안된 방법으로 GIoU가 (Generalized IoU) 가 있다고,,,
- [here](https://hongl.tistory.com/215) 여기 보고 더 찾아보자



## 추가 하고 싶은 것들
### [RBox](https://dl.acm.org/doi/pdf/10.1145/3274895.3274915)
- RBox-CNN Rotated Bounding Box
- RBox (x, y, h, w, theta(시계 반대방향으로 돌아간 정도{-pi/2, pi/2})) 
- RBox regression 방법 smooth loss 는 Fast R-CNN의 정의와 같은 내용이다
- 
