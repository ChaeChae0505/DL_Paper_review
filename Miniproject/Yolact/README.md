# 사용법

[참고하기](https://ksg980920.tistory.com/2)


conda 환경 : YOLACT python3.7

$ conda activate yolact

# Cython needs to be installed before pycocotools
pip install cython
pip install opencv-python pillow pycocotools matplotlib 





$ git clone https://github.com/dbolya/yolact.git





## cuda 확인 방법
```
import torch
torch.cuda.is_available()
torch.cuda.current_device()
torch.cuda.get_device_name(0)
```

## Taining , eval


# error1
dataloader - suffle 기능 false로 변경
https://github.com/dbolya/yolact/issues/664


# error 2 
OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized

 이미지 데이터 셋을 pyplot 시각화 할 때 뜨는 에러임 
import os
os.environ['KMP_DUPLICATE_LIB_OK']='True' 돌리고 해야함

