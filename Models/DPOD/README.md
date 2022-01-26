- 우선 all_images_adr.pkl , train_images_indices.pkl , test_images_indices.pkle 파일로 나뉘어 지는 것 같다

# eval.py 분석 

- test_img : 자른 pkl 파일에서 불러온 test img 인거 같다 , pred_pos는 xy, z, rot를 변형해서 만들어준 거 같고, true pose는 진짜 포즈이다.
- 어떻게 이걸 시각화 할 것인가?
- 1) test_img를 정상적인 색으로 불러 온다
- 2) pred_pose와 true pose
