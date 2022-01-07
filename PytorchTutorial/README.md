# Object detection
- [Link](https://github.com/sgrvinod/a-PyTorch-Tutorial-to-Object-Detection)
- 종류 : Single-shot Detection
- 수행 기간 : 22.01.06 ~
- 실행시키기위해서!
(1) VOC dataset download


#### 1. VOC dataset
- http://host.robots.ox.ac.uk/pascal/VOC/voc2012/
- http://host.robots.ox.ac.uk/pascal/VOC/voc2007/
- 

### git을 파기전에 궁금한 개념들
- bounding box는 왜 필요?
- NMS 도대체 뭐?
- WBF는?
- Anchor box가 없는 모델은??  Anchor free
- *Selective Search* 
- Multi object detection 
- 엥 two stage detector랑 one stage detector 를 구별하는 기준은 알겠는데 실제로 어떻게 다르게 동작하는 거지?
- 한번 봤던 내용인데 이해가 안 되는 거는,,, 내가 공부를 제대로 안했다는 말,,,, 이번에 코드도 같이 보자



- 근데 사실 object detection에서는 클래스, cx,cy(센터값), h, w(가로세로) 좌표를 regression하는 것과 같다. 근데 anchor box가 왜 필요한가?
- [Andrew ang님의 강의를 참고](https://www.youtube.com/watch?v=XdsmlBGOK-k)
1. *Sliding windows* 
- 방식은 box를 이동하면서 위치를 찾는 방법인데 딥러닝 이전에도 많이 쓰이고, object detection 시에도 가끔 등장
- 계산 비용이,,, 많이 든다는데 convenet을 통해 각각을 독립적으로 실행 시킨다? Convolutional Implementation of sliding windows등장
- 아 각 각 하는건 똑같은데 끝에 conv를 fc로 만드냐 텐서로 만드냐의 차인가?

2. Anchor Boxes
- Object detection은 각각의 grid cell이 오직 하나의 object 만 감지 할 수 있다! grid cell이 여러개의 object 를 감지 해야할때! 즉 object 끼리 서로 겹쳐 있을 때 (overlapping object)
- 각 클래스 별로 Anchor box를 지정하여,
3. 
4. 


## Single-shot detection 특징

