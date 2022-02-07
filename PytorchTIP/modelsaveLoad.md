## torch model save method
1. torch.save(path, model)
- 모델 전체 저장
- model = torch.load(path) 
2. torch.save(path, model.state_dict())
- model 안에 파라미터 저장
