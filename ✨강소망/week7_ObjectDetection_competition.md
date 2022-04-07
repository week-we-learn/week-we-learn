# Object Detection

Created: January 17, 2022 2:09 PM

**Baseline code**

- mmDetection
- yolov5 → mmDetection 찾을 수 없어서 github clone

**사용기법**

- Augmentation
- Ensemble

**사용 Tool**

- WandB
    
    → [https://wandb.ai/somang/YOLOv5?workspace=user-somang](https://wandb.ai/somang/YOLOv5?workspace=user-somang)
    
- Notion
- tmux
    
    → 서버 접속 후 모델 실행하고 컴퓨터를 꺼도 학습이 계속된다!
    

**시도 과정**

1. faster RCNN
    
    ⇒ mmDetection 그대로 사용
    
    - mAP50 0.4...
2. Cascade RCNN
    
    ⇒ mmDetection 그대로 사용
    
    - mAP50 0.5
3. Yolox_x
    
    ⇒ mmDetection 그대로 사용
    
    - 300epoch → 약 30h 소요
    - mAP50 0.42
4. Yolov5x6
    
    ⇒ yolov5 파이토치 구현 코드 이용
    
    - epoch 36 → 연결끊김
    
    ⇒ Augmentation 적용1
    
    - epoch 100 → 약 10h 소요
    - mAP50 5.6
    
    ⇒ Augmentation 적용2
    
    - epoch 100
    - mAP50