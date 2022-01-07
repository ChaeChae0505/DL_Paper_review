# Object detection
- [Link](https://github.com/sgrvinod/a-PyTorch-Tutorial-to-Object-Detection)
- 종류 : Single-shot Detection
- 수행 기간 : 22.01.06 ~
- 실행시키기위해서!
(1) VOC dataset download


#### 1. VOC dataset
- http://host.robots.ox.ac.uk/pascal/VOC/voc2012/
- http://host.robots.ox.ac.uk/pascal/VOC/voc2007/
- <img src="https://github.com/ChaeChae0505/TIL_STUDY/blob/main/Image/VOC.JPG" width="50%" height="50%">
- 위에 꺼처럼 다운 받는다
- 다운 받고 압축을 풀면, tar이라서 windows에서는 반디집 깔아야 풀 수 있다
- 아래 처럼 Annotation이 되있는 것을 확인 할 수 있다
- <img src="https://github.com/ChaeChae0505/TIL_STUDY/blob/main/Image/pascal.JPG" width="50%" height="50%">

#### 2. Inputs to model
- SSD300을 할껀데 input image size가 300, 300이란 말이다. 
- VGG-16 pretrained on ImageNet 을 사용할 것이다 pytorch의 torchivision module에 있다

##### Images
- Imagenet을 pre-trained로 사용할 것인데 그래서 정규화 필요! [0,1]로 
- image 는 NCHW로 되어있는데 [batch size, channel, height, width]

##### Object's Bounding Boxes
- (x_min, y_min, x_max, y_max)

##### Object's Labels
- background class 0 


##### Data pipline
- training 과 test로 splits
1. Parse raw data
- create_data_lists() in utils.py
- Create lists path --> create_data_lists path 변경
```python
def create_data_lists(voc07_path, voc12_path, output_folder):
    """
    Create lists of images, the bounding boxes and labels of the objects in these images, and save these to file.

    :param voc07_path: path to the 'VOC2007' folder
    :param voc12_path: path to the 'VOC2012' folder
    :param output_folder: folder where the JSONs must be saved
    """
    voc07_path = os.path.abspath(voc07_path)
    voc12_path = os.path.abspath(voc12_path)

    train_images = list()
    train_objects = list()
    n_objects = 0

    # Training data
    for path in [voc07_path, voc12_path]:

        # Find IDs of images in training data
        with open(os.path.join(path, 'ImageSets/Main/trainval.txt')) as f:
            ids = f.read().splitlines()

        for id in ids:
            # Parse annotation's XML file
            objects = parse_annotation(os.path.join(path, 'Annotations', id + '.xml'))
            if len(objects['boxes']) == 0:
                continue
            n_objects += len(objects)
            train_objects.append(objects)
            train_images.append(os.path.join(path, 'JPEGImages', id + '.jpg'))

    assert len(train_objects) == len(train_images)

    # Save to file
    with open(os.path.join(output_folder, 'TRAIN_images.json'), 'w') as j:
        json.dump(train_images, j)
    with open(os.path.join(output_folder, 'TRAIN_objects.json'), 'w') as j:
        json.dump(train_objects, j)
    with open(os.path.join(output_folder, 'label_map.json'), 'w') as j:
        json.dump(label_map, j)  # save label map too

    print('\nThere are %d training images containing a total of %d objects. Files have been saved to %s.' % (
        len(train_images), n_objects, os.path.abspath(output_folder)))

    # Test data
    test_images = list()
    test_objects = list()
    n_objects = 0

    # Find IDs of images in the test data
    with open(os.path.join(voc07_path, 'ImageSets/Main/test.txt')) as f:
        ids = f.read().splitlines()

    for id in ids:
        # Parse annotation's XML file
        objects = parse_annotation(os.path.join(voc07_path, 'Annotations', id + '.xml'))
        if len(objects) == 0:
            continue
        test_objects.append(objects)
        n_objects += len(objects)
        test_images.append(os.path.join(voc07_path, 'JPEGImages', id + '.jpg'))

    assert len(test_objects) == len(test_images)

    # Save to file
    with open(os.path.join(output_folder, 'TEST_images.json'), 'w') as j:
        json.dump(test_images, j)
    with open(os.path.join(output_folder, 'TEST_objects.json'), 'w') as j:
        json.dump(test_objects, j)

    print('\nThere are %d test images containing a total of %d objects. Files have been saved to %s.' % (
        len(test_images), n_objects, os.path.abspath(output_folder)))
```

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

