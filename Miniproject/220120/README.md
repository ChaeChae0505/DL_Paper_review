- Box를 검출하는 알고리즘 
1. Box를 bounding box를 통해 검출한다.
2. Box를 segmentation을 통해 검출한다


## Purpose
- Yolo 구현을 목표로 하여 custom dataset인 box에 적용해본다 -> center 파지점도 검출.
- 먼저 이런 멋진 [Tutorial](https://blog.paperspace.com/how-to-implement-a-yolo-object-detector-in-pytorch/) 의 존재에 감사하며 이걸 먼저 따라 해보기로 함. [Full code](https://github.com/ayooshkathuria/YOLO_v3_tutorial_from_scratch)
- 한국어 번역 version [here](https://deep-learning-study.tistory.com/411)
- 구성은 다음과 같음 
1. Understanding How YOLO works
2. Creating the layers of the network architecture
3. Implementing the the forward pass of the network
4. Objectness score thresholding and Non-maximum suppression
5. Designing the input and the output pipelines
- 이외에 custom dataset 사용을 위해 추가로 Data 포맷 및 load 방법을 알아볼 것이다

---
## Understanding How YOLO works
### Prerequisties
- 먼저 CNN이 어떻게 동작하는지  Residual Blocks, skip connections, upsampling 에 대해 이해하고 있다는 전제에서 시작한다
- Object detection이 무엇이고, bounding box regression, IoU 그리고 Non-maximum suppression이 무엇인지 알아야한다.
#### NMS(Non-maximum suppression)
- Input image가 object detection 알고리즘 통과 후 bbox가 그려지면 어떤 물체일 확률 값을 가지게 되는데 이때 object 위에 생기는 많은 bbox에 대해 가장 스코어가 높은 박스만 남기고 나머지를 제거하는 것이 NMS 이다.
- NMS 의 Input은 B(bbox list),S(bbox의 confidence scores),N 중첩 임계값 / Output은 D 필터링된 bbox list   
- code [1](https://github.com/amusi/Non-Maximum-Suppression/blob/master/nms.py)[2](https://heiwais25.github.io/machine%20learning/cnn/2018/05/10/non-maximum-suppression/)
- [자세한 설명 with code](https://towardsdatascience.com/non-maxima-suppression-139f7e00f0b5)  

**Algorithm**  
1. Confidence가 가장 높은 것을 선택하고 B에서 제거한 다음 D에 추가 함
2. 모든 B를 비교하고 IoU를 계산 한다 IoU가 임계값 N보다 큰 경우 B에서 해당 B를 제거 한다
3. 다시 B의 나머지 Box에서 confidence가 높은 제안을 B에서 제거하고 D에 추가한다
4. 다시 한번 B의 모든 Box로 IoU를 계산하고 임계값 보다 IoU가 높은 상자를 제거함
5. B에 더이상 box 제안이 남아있지 않을 때 까지 반복한다



```python
# Felzenszwalb et al
def non_max_suppression_fast(boxes, scores, iou_threshold):
	'''
		boxes : coordinates of each box
		scores : score of each box
		iou_threshold : iou threshold(box with iou larger than threshold will be removed)
	'''
	if len(boxes) == 0:
		return []
	
	# Init the picked box info
	pick = []
	
	# Box coordinate consist of left top and right bottom
	x1 = boxes[:,0]
	y1 = boxes[:,1]
	x2 = boxes[:,2]
	y2 = boxes[:,3]

	# Compute area of each boxes
	area = (x2 - x1 + 1) * (y2 - y1 + 1)
	# Greedily select the order of box to compare iou
	idxs = np.argsort(scores)
	
	while(len(idxs) > 0):
        last = len(idxs) - 1
        i = idxs[last]
        pick.append(i)
        
        # With vector implementation, we can calculate fast
        xx1 = np.maximum(x1[i], x1[idxs[:last]])
        yy1 = np.maximum(y1[i], y1[idxs[:last]])
        xx2 = np.minimum(x2[i], x2[idxs[:last]])
        yy2 = np.minimum(y2[i], y2[idxs[:last]])

        w = np.maximum(0, xx2 - xx1 + 1)
        h = np.maximum(0, yy2 - yy1 + 1)
        intersection = w * h
        
		# Calculate the iou
        iou = intersection / (area[idxs[:last]] + area[idxs[last]] - intersection)
        
        idxs = np.delete(idxs, np.concatenate(([last], np.where(iou > iou_threshold)[0])))
        
    return boxes[pick].astype("int")
```




### What is Yolo

### A Fully Convolutional Neural Network
- Yolo는 FCN(Fully convolutional network)로 만들어져있다. Upsampling layers와 skip connection을 지니 75개의 conv layers로 구성되어있다. Pooling 이 사용되지 않으며, feature maps를 downsample 하기 위해서 2stride의 conv layer가 사용되었다. 이를 통해 pooling 사용으로 인한 low-level features의 손실을 방지할 수 있다.
- FCN으로 구성되어있기 때문에 Yolo는 이미지 사이즈에 국한되지 않지만, 학습시에 이미지 사이즈를 고정해서 줍니다. heads에서 보이는 다양한 문제 때문에??
- 

