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
