- 검색으로 어느정도 이해는 할 수 있지만 전반적으로 어떻게 구성되는지 알 필요가 있는거 같다
- 책을 통해서 deep learning model에 대한 구현을 pytorch에서 어떤식으로 동작시키는지 알아보자
# 다음 순서를 기반으로 공부
1. [한국어 tutorial](https://tutorials.pytorch.kr/)
2. 아니 이렇게 좋은 [자료](https://github.com/sgrvinod/Deep-Tutorials-for-PyTorch)가
#### 추가 참고
- [wiki docs 책 참고](https://wikidocs.net/57168)
- [youtube참고](https://www.youtube.com/channel/UCK24Wy_G-6V-quKvVRjflgA/videos)목차 참고 하기로 했다.
---
## pytorch document tutorial
목차  
0. [빠른 시작](#0.빠른-시작)
1. 텐서(Tensor)
2. Dataset과 DataLoader
3. 변형(Transform)
4. 신경망 모델 구성하기
5. 자동 미분(Automatic Differentiation)
6. 최적화 단계(Optimization Loop)
7. 모델 저장하고 불러오고 사용하기


### 0.빠른 시작
#### 데이터 작업하기
- 데이터 작업을 위한 기본 요소 1)*torch.utils.data.Dataset* 2)*torch.utils.data.DataLoader* 이 있다. PyTorch는 TorchText, [TorchVision](https://pytorch.org/vision/stable/index.html) 및 TorchAudio같은 데이터셋도 제공하고 있음

1)*torch.utils.data.Dataset* : 샘플과 정답(label)을 저장[참고](https://pytorch.org/vision/stable/datasets.html) 
- 사용할 수 있는 [dataset 목록](https://pytorch.org/vision/stable/datasets.html)
2) *torch.utils.data.DataLoader* : Dataset을 순회 가능한 객체(iterable)로 감쌈  

#### 모델 만들기
#### 모델 매개변수 최적화하기
#### 모델 저장하기
#### 모델 불러오기

### 1.Tensor
### 2.Dataset과 Dataloader
### 3.Transform
### 4.신경망 모델 구성하기 
### 5.Autograd
### 6.최적화(Optimization)
### 7.모델 저장하고 불러오기
---

