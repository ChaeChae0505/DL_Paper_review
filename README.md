# DL Paper_review
- Paper review 및 model 구현 내용에 대해 작성합니다.
- 모델 구현 ! 은 TIL_DL_NEW/ Models / vit / modelname.ipynb 로 보내고, README에다 정리하자
---
### To-Do List 
|공부기간|Model|Paper|Code|
|:----|:----|:---:|:------:|
|220105 ~|[ViT](https://arxiv.org/pdf/2010.11929.pdf)|❌|❌|
||
😆✔️✔️
🙂❌✔️
😡❌❌

---
# Pytorch TIP
- 기타 pytorch tip은 TIL_DL_NEW/README.md 에 적자
  - pytorch model 생성 팁 참고
  - [1][https://gaussian37.github.io/dl-pytorch-snippets/](https://gaussian37.github.io/dl-pytorch-snippets/)
  - [2][https://anweh.tistory.com/21](https://anweh.tistory.com/21)
  - [3][예제로 배우는 pytorch](https://tutorials.pytorch.kr/beginner/pytorch_with_examples.html)
  - [4][Pytorch 활성화 함수의 종류](https://pytorch.org/docs/stable/nn.html#non-linear-activations-weighted-sum-nonlinearity)
  - [5][paper review](https://github.com/Seonghoon-Yu/AI_Paper_Review)

## 목차  
[신경망 모델 정의하는 방법](#신경망-모델-정의하는-방법)  
[차원관리einops](#차원관리)  
[torch.cat](#torch-cat)  

---

## 신경망 모델 정의하는 방법 
- [참고1](https://anweh.tistory.com/21)
- [참고2](https://data-panic.tistory.com/15)
- [wikidocs pytorch로 시작하는 딥러닝 입문](https://wikidocs.net/60036)
```
@ Pytorch 신경망 설계 방법
1. 사용자 정의 nn 모듈
2. nn.Module 상속한 클래스 이용
- class로 선언할 때 __init__과 forward는 필수!
- forward에서 H(x)에 입력 x로 부터 예측된 결과 y를 얻게 해줌!


@ pytorch로 신경망 모델 설계 시 Step
1. Design your model using class with Variables
2. Construct loss and optim
3. Train cycle(forward, backwoard, update)
```

## nn.Sequential 과 nn.ModuleList 차이
- 이해가 어렵다 대충 이해 했을 때 sequential은 모델들을 순차적으로 합칠 수 있는 듯 하다 [참고](https://michigusa-nlp.tistory.com/26) 다시 읽어보자

## 차원관리
- ViT code를 보다 알게 되었다.
```
from einops import rearrange, reduce, repeat
# rearrange elements according to the pattern
output_tensor = rearrange(input_tensor, 't b c -> b c t')
# combine rearrangement and reduction
output_tensor = reduce(input_tensor, 'b c (h h2) (w w2) -> b h w c', 'mean', h2=2, w2=2)
# copy along a new axis 
output_tensor = repeat(input_tensor, 'h w -> h w c', c=3)
```
- str로 차원 관리를 한다는게 익숙하지는 않지만, 그래도 엄청 직관적인 것 같다

## torch cat
- casting 하는 존재인 거 같다
> torch.cat(tensors, dim=0, *, out=None) 

```
Parameters
tensors (sequence of Tensors) – any python sequence of tensors of the same type. Non-empty tensors provided must have the same shape, except in the cat dimension.

dim (int, optional) – the dimension over which the tensors are concatenated

Keyword Arguments
out (Tensor, optional) – the output tensor.
```

```python
>>> x = torch.randn(2, 3)
>>> x
tensor([[ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497]])
>>> torch.cat((x, x, x), 0)
tensor([[ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497],
        [ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497],
        [ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497]])
>>> torch.cat((x, x, x), 1)
tensor([[ 0.6580, -1.0969, -0.4614,  0.6580, -1.0969, -0.4614,  0.6580,
         -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497, -0.1034, -0.5790,  0.1497, -0.1034,
         -0.5790,  0.1497]])
```
