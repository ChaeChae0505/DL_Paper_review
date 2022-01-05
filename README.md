# DL Paper_review
- Paper review 및 model 구현 내용에 대해 작성합니다.
- 모델 구현 ! 은 TIL_DL_NEW/ Models / vit / modelname.ipynb 로 보내고, README에다 정리하자
- 기타 pytorch tip은 TIL_DL_NEW/README.md 에 적자
  - pytorch model 생성 팁 참고
  - [1][https://gaussian37.github.io/dl-pytorch-snippets/](https://gaussian37.github.io/dl-pytorch-snippets/)
  - [2][https://anweh.tistory.com/21](https://anweh.tistory.com/21)
  - [3][예제로 배우는 pytorch](https://tutorials.pytorch.kr/beginner/pytorch_with_examples.html)
  - [4][Pytorch 활성화 함수의 종류](https://pytorch.org/docs/stable/nn.html#non-linear-activations-weighted-sum-nonlinearity)
  - [5][paper review](https://github.com/Seonghoon-Yu/AI_Paper_Review)
---
### To-Do List 
|Model|Paper|Code|
|:----|:---:|:------:|
|[ViT](https://arxiv.org/pdf/2010.11929.pdf)|❌|❌|
||
😆✔️✔️
🙂❌✔️
😡❌❌

---
목차  
[신경망 모델 정의하는 방법](#신경망-모델-정의하는-방법) 

---

## 신경망 모델 정의하는 방법 
```
@ Pytorch 신경망 설계 방법
1. 사용자 정의 nn 모듈
2. nn.Module 상속한 클래스 이용


@ pytorch로 신경망 모델 설계 시 Step
1. Design your model using class with Variables
2. Construct loss and optim
3. Train cycle(forward, backwoard, update)
```






