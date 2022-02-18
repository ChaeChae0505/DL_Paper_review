*--version 22.01.15--*

# 220103
- PoseCNN을 어떻게든 돌려보자 
- https://hub.docker.com/r/celinachild/floam-ssl 을 다운 받아서 
- 그위에 형기님 cpp ++ 한 후 저장 https://github.com/changh95/cpp-cv-project-template
- PoseCNN 다운 해서 돌려보자! https://github.com/NVlabs/PoseCNN-PyTorch
- tmux https://www.cv-learn.com/20210912-ros-tutorials-1/?highlight=docker



-- 위의 과정을 끝낸 후 
-- Docker를 새로운 이미지에 저장할 것이다.
```
# docker images check sudo docker images 
# Image 실행 
sudo docker run -it <images name> 
# docker 수정 
# docker를 실행한 채로 
# 다른 터미널에서 
sudo docker ps 
# Container ID 항목 복사 
sudo docker commit <container ID> <New image save name> 
# 이미지 실행가능해짐

```

> 오늘 진행한 것 
- docker  docker.io/celinachild/floam-ssl:latest 다운 받았음
- posecnn 공부 조금 하다가 module부분을  찾다가 TIL deeplearning > module > 신경망모델 정의 쪽으로 가서 확인하기 
- A4 용지 확인하기 
- https://gaussian37.github.io/dl-pytorch-snippets/ 이거 한번 보면서 공부해보자



# 220110
- https://github.com/kirumang/NOL 이거 해보기로 했다
- docker_run.sh를 통해 smot 데이터가 있는 dir를 연결한다 (https://tttsss77.tistory.com/161)
- 2022-01-10 04:28:35.998425: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libnvinfer.so.6'; dlerror: libnvinfer.so.6: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /usr/lib/x86_64-linux-gnu:/usr/lib/i386-linux-gnu:/usr/local/nvidia/lib:/usr/local/nvidia/lib64:/usr/local/nvidia/lib:/usr/local/nvidia/lib64
error가 나서 아래 설치를 해줌
- pip install tf-nightly


- 딱히 ubuntu로 빌드할 필요가 없다면,,, 그냥 ananaconda에 올려보자


# 220112
```
 Total number of images:  15801
 Total number of training images:  2370
 Total number of testing images:  13431
------ Start creating ground truth ------
0/2370 finished!
1000/2370 finished!
2000/2370 finished!
----- Finished creating ground truth -----
------ Started training of the correspondence block ------
------ Epoch  1  ---------
/home/ch/KITECH/DPOD/unet_model.py:63: UserWarning: __floordiv__ is deprecated, and its behavior will change in a future version of pytorch. It currently rounds toward 0 (like the 'trunc' function NOT 'floor'). This results in incorrect rounding for negative values. To keep the current behavior, use torch.div(a, b, rounding_mode='trunc'), or for actual floor division, use torch.div(a, b, rounding_mode='floor').
  x1 = F.pad(x1, [diffX // 2, diffX - diffX // 2,
/home/ch/KITECH/DPOD/unet_model.py:64: UserWarning: __floordiv__ is deprecated, and its behavior will change in a future version of pytorch. It currently rounds toward 0 (like the 'trunc' function NOT 'floor'). This results in incorrect rounding for negative values. To keep the current behavior, use torch.div(a, b, rounding_mode='trunc'), or for actual floor division, use torch.div(a, b, rounding_mode='floor').
  diffY // 2, diffY - diffY // 2])
Epoch: 1        Training Loss: 0.274526         Validation Loss: 0.130229
Validation loss decreased (inf --> 0.130229).  Saving model ...
------ Epoch  2  ---------
Epoch: 2        Training Loss: 0.118506         Validation Loss: 0.159900
------ Epoch  3  ---------
Epoch: 3        Training Loss: 0.104805         Validation Loss: 0.097147
Validation loss decreased (0.130229 --> 0.097147).  Saving model ...
------ Epoch  4  ---------
Epoch: 4        Training Loss: 0.095050         Validation Loss: 0.093446
Validation loss decreased (0.097147 --> 0.093446).  Saving model ...
------ Epoch  5  ---------
Epoch: 5        Training Loss: 0.087498         Validation Loss: 0.082488
Validation loss decreased (0.093446 --> 0.082488).  Saving model ...
------ Epoch  6  ---------
Epoch: 6        Training Loss: 0.082059         Validation Loss: 0.118974
------ Epoch  7  ---------
Epoch: 7        Training Loss: 0.078437         Validation Loss: 0.076966
Validation loss decreased (0.082488 --> 0.076966).  Saving model ...
------ Epoch  8  ---------
Epoch: 8        Training Loss: 0.076331         Validation Loss: 0.084126
------ Epoch  9  ---------
Epoch: 9        Training Loss: 0.073715         Validation Loss: 0.072284
Validation loss decreased (0.076966 --> 0.072284).  Saving model ...
------ Epoch  10  ---------
Epoch: 10       Training Loss: 0.071835         Validation Loss: 0.072434
------ Epoch  11  ---------
Epoch: 11       Training Loss: 0.070368         Validation Loss: 0.072816
------ Epoch  12  ---------
Epoch: 12       Training Loss: 0.069222         Validation Loss: 0.075397
------ Epoch  13  ---------
Epoch: 13       Training Loss: 0.068191         Validation Loss: 0.069796
Validation loss decreased (0.072284 --> 0.069796).  Saving model ...
------ Epoch  14  ---------
Epoch: 14       Training Loss: 0.065972         Validation Loss: 0.067884
Validation loss decreased (0.069796 --> 0.067884).  Saving model ...
------ Epoch  15  ---------
Epoch: 15       Training Loss: 0.067252         Validation Loss: 0.067641
Validation loss decreased (0.067884 --> 0.067641).  Saving model ...
------ Epoch  16  ---------
Epoch: 16       Training Loss: 0.065304         Validation Loss: 0.071574
------ Epoch  17  ---------
Epoch: 17       Training Loss: 0.064280         Validation Loss: 0.067426
Validation loss decreased (0.067641 --> 0.067426).  Saving model ...
------ Epoch  18  ---------
Epoch: 18       Training Loss: 0.062575         Validation Loss: 0.067714
------ Epoch  19  ---------
Epoch: 19       Training Loss: 0.064320         Validation Loss: 0.064951
Validation loss decreased (0.067426 --> 0.064951).  Saving model ...
------ Epoch  20  ---------
Epoch: 20       Training Loss: 0.062200         Validation Loss: 0.069111
------ Training Finished ------
------ Started Initial pose estimation ------
0/2370 finished!
1000/2370 finished!
2000/2370 finished!
Number of instances where PnP couldn't be used:  211
------ Finished Initial pose estimation -----
----- Started creating inputs for DL based pose refinement ------
0/2370 finished!
/home/ch/KITECH/DPOD/create_renderings.py:31: RuntimeWarning: overflow encountered in true_divide
  coord_2D = homogenous_2D[:2, :] / homogenous_2D[2, :]
1000/2370 finished!
2000/2370 finished!
Number of outliers:  26
----- Finished creating inputs for DL based pose refinement
----- Started training DL based pose refiner ------
Downloading: "https://download.pytorch.org/models/resnet18-f37072fd.pth" to /home/ch/.cache/torch/hub/checkpoints/resnet18-f37072fd.pth
100.0%
----- Epoch Number:  1 --------
Traceback (most recent call last):
  File "train.py", line 82, in <module>
    train_pose_refinement(root_dir, classes, epochs=10)
  File "/home/ch/KITECH/DPOD/pose_refinement.py", line 147, in train_pose_refinement
    xy, z, rot = pose_refiner(image, rendered, pred_pose, batch_size)
  File "/home/ch/KITECH/DPOD/venv/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ch/KITECH/DPOD/pose_refiner_architecture.py", line 63, in forward
    z = self.fc_zhead(f)
  File "/home/ch/KITECH/DPOD/venv/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ch/KITECH/DPOD/venv/lib/python3.8/site-packages/torch/nn/modules/container.py", line 141, in forward
    input = module(input)
  File "/home/ch/KITECH/DPOD/venv/lib/python3.8/site-packages/torch/nn/modules/module.py", line 1102, in _call_impl
    return forward_call(*input, **kwargs)
  File "/home/ch/KITECH/DPOD/venv/lib/python3.8/site-packages/torch/nn/modules/linear.py", line 103, in forward
    return F.linear(input, self.weight, self.bias)
  File "/home/ch/KITECH/DPOD/venv/lib/python3.8/site-packages/torch/nn/functional.py", line 1848, in linear
    return torch._C._nn.linear(input, weight, bias)
RuntimeError: mat1 and mat2 shapes cannot be multiplied (4x256 and 512x256)
```


UNET model 변경
```
    def forward(self, x1, x2):
        x1 = self.up(x1)
        # input is CHW
        diffY = torch.tensor([x2.size()[2] - x1.size()[2]])
        diffX = torch.tensor([x2.size()[3] - x1.size()[3]])

        # x1 = F.pad(x1, [diffX // 2, diffX - diffX // 2,
        #                 diffY // 2, diffY - diffY // 2])

        x1 = F.pad(x1, [torch.div(diffX, 2, rounding_mode='floor'), torch.div(diffX - diffX, 2, rounding_mode='floor'),
                        torch.div(diffY, 2, rounding_mode='floor'), torch.div(diffY - diffY, 2, rounding_mode='floor')])

        x = torch.cat([x2, x1], dim=1)
        return self.conv(x)

```


RuntimeWarning: overflow encountered in true_divide

conda deactivate : conda config --set auto_activate_base false



> ValueError: unsupported pickle protocol: 5
- version 문제 임으로 python 3.7이상 쓰길 바란다



# 220113
- 드디어 DPOD의 문제가 되는 지점을 발견했다 
```
checking image 116 ('glue', 'lamp', 'iron', 'holepuncher')
here1
torch.Size([4, 3, 224, 224]) torch.Size([4, 3, 224, 224]) torch.Size([4, 3, 4])
here2
1
2
3
4
5
checking image 117 ('iron', 'ape', 'cat', 'can')
here1
image.shape, rendered.shape, pred_pose.shape 
torch.Size([2, 3, 224, 224]) torch.Size([2, 3, 224, 224]) torch.Size([2, 3, 4])

5016
4608
데이터 갯수가 좀 다른 듯 하다

엥 근데 아까도 다른거 였는데 여기서 멈췄다 
Traceback (most recent call last):

  File "/home/ch/KITECH/DPOD/train2.py", line 83, in <module>
    train_pose_refinement(root_dir, classes, epochs=10)
```


# 220114
- 원래 배치 사이즈에 영향을 받지 않아야한다고,,, loader 파트에서 drop_last true해ㅂ자
- batch 사이즈에 영향을 받게 설계되어 있다면 drop_last =  True를 하면 된다 batch size에 의존도가 높은 경우 마지막 batch를 사용하지 않는 것 

- eval.py를 돌리려고 하는데 채널 순서가 이상했다 그래서 

```python
       # check number of channels
        if pic.shape[-3] > 4:
            raise ValueError('pic should not have > 4 channels. Got {} channels.'.format(pic.shape[-3]))
```

이렇게 되어있길래         obj_img = obj_img.squeeze().transpose(0, 2).transpose(0,1) 되어있던 것을 { (1,3,240,320) --> (240,320,3)}
>> squeeze().transpose(1,2)로 바꿔 줬다{(1,3,240,320) --> (3,320,240)}

- ADD Score for all testing images is:  0.4555133646042737 이런 결과를 얻었는데 확인할 방법이 없다
- 그리고 pt 파일이 만들어 졌는데 어떻게 만들어졌는지 알 수가 없다


helper에 bounding box 부분 인거 같은데 도대체 이걸 어떻게 사용하냐,,,



# 220125
- pt 파일은 save 파일 이였다 역시

- DPOD : https://github.com/zakharos/DPOD/blob/b33773bac5b3ce13b2e9fe457c908dfac0a4f275/utils/visualization.py#L11 를 보면 힌트를 얻을 수 있을 거 같다 


3D visualization을 하기 위해서!
```
gt_bbs라는 list 로 들어가는데 
gt_transformed_bb를 인자로 받고 있는 list이다

# Estimated bounding box
bb3d = eval.init_3d_bbox(testset.model)
transformed_bb = eval.project_points(bb3d, predicted_pose, cam)
transformed_bb = np.transpose(transformed_bb, (1, 0))
pnp_bbs.append(transformed_bb)
all_distances.append(best_distance)

# Ground truth bounding box
gt_transformed_bb = eval.project_points(bb3d, gt_pose, cam)
gt_transformed_bb = np.transpose(gt_transformed_bb, (1, 0))

```
