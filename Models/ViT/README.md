- 논문 : An Image is worth 16x16 words : Transformers for Image Recognition at Scale
- 분류 : Transformer
- 저자 : Alexey Dosovitskiy, , Lucas Beyer , Alexander Kolesnikov , Dirk Weissenborn
- 읽는 배경 : Visoin Transformers 가 도대체 뭔지 알아보기. 
- 느낀점 : Transformer의 기초를 읽어보자 attention all ~
- 공부 참고자료
- [1][Yotube](https://www.youtube.com/watch?v=TrdevFK_am4&t=847s)
- [2][CODE vit-pytorch](https://github.com/lucidrains/vit-pytorch)
- [3][CODE easy](https://towardsdatascience.com/implementing-visualttransformer-in-pytorch-184f9f16f632)
---
요약 
- vision task에서 Transformer를 사용해서 잘 작동하게 만들었다
---


## Method
- Transformer encoder 부분은 어떻게 만들었을까?
#### Method 요약
1. Patch Embedding
- linear layer화 시킨다 patchembedding?
- Position을 embedding 시킨다 원래 위치에 대한 정보를 주는 듯
2. MultiHead Attention
3. Residual
4. FeedForwardBlock
5. TransformerEncoderBlock
6. TransformerEncoder
7. ClassificationHead
8. ViT
