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


# error1
dataloader - suffle 기능 false로 변경
https://github.com/dbolya/yolact/issues/664


# error 2 
OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized

 이미지 데이터 셋을 pyplot 시각화 할 때 뜨는 에러임 
import os
os.environ['KMP_DUPLICATE_LIB_OK']='True' 돌리고 해야함


Calculating mAP...

       |  all  |  .50  |  .55  |  .60  |  .65  |  .70  |  .75  |  .80  |  .85  |  .90  |  .95  |
-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+
   box | 14.36 | 27.94 | 27.75 | 27.28 | 24.51 | 18.52 | 11.15 |  4.82 |  1.23 |  0.36 |  0.04 |
  mask | 22.42 | 28.30 | 27.98 | 27.98 | 27.62 | 27.60 | 27.26 | 24.03 | 18.99 | 12.32 |  2.09 |
-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+-------+

