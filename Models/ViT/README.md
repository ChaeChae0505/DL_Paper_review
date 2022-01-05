- 정확히 이해하지 못한 부분 %
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
- 
1. Patch Embedding
- 이미지를 받아서
- 16x16으로 patch를 자른다 
- 각 patch를 1D-vector로 풀어냄
- 1D-vector로 만들어진 pacth들을 Linear Projection을 통해 768차원의 각 patch의 embedding vector로 표현
- 각 patch embedding에 classification token, position embedding 추가
  - Position embedding : patch의 위치 정보를 가지고 있는 embedding , position embedding을 사용하지 않으면 이미지의 입력-> 일전 크기의 patch로 자름 -> patch를 sequence로 생각하여 transformer encoder로 입력 -> 각 patch의 위치 정보 손실 -> 학습 불가
  - classification token, position token은 학습에 의해 결정되는 parameter라는데 왜? %
```python
class PatchEmbedding(nn.Module):
    def __init__(self, in_channels=3, patch_size=16, emb_size=768, img_size=224):
        super().__init__()
        self.patch_size = patch_size

        # # Method 1: Flatten and FC layer
        # self.projection = nn.Sequential(
        #     Rearrange('b c (h s1) (w s2) -> b (h w) (s1 s2 c)', s1=patch_size, s2=patch_size),
        #     nn.Linear(path_size * patch_size * in_channels, emb_size)
        # )

        # Method 2: Conv
        self.projection = nn.Sequential(
            # using a conv layer instead of a linear one -> performance gains
            nn.Conv2d(in_channels, emb_size, patch_size, stride=patch_size),
            Rearrange('b e (h) (w) -> b (h w) e')
        )

        # cls_token batch time
        self.cls_token = nn.Parameter(torch.randn(1,1,emb_size))
        # Position embedding 
        self.positions = nn.Parameter(torch.randn((img_size // patch_size) ** 2 + 1, emb_size))

    def forward(self, x):
        
        b = x.shape[0]
        x = self.projection(x)
        cls_tokens = repeat(self.cls_token, '() n e -> b n e', b=b)
        
        # prepend the cls token to the input
        x = torch.cat([cls_tokens, x], dim=1)
        
        # add position embedding to prejected patches
        x += self.positions
        return x
```
2. MultiHead Attention
3. Residual
4. FeedForwardBlock
5. TransformerEncoderBlock
6. TransformerEncoder
7. ClassificationHead
8. ViT
