# 차량 운전자 부주의 행동 분류를 위한 경량 CNN 비교

정우제\*

# Comparison of Lightweight CNNs for Driver Distraction Classification

Woo-Je Jeong\*

\*국립한국교통대학교 컴퓨터공학부 인공지능공학과
e-mail: wjddnwp29@kumoh.ac.kr

---

## 요  약

본 논문에서는 차량 운전자 모니터링 시스템(DMS)에 사용할 수 있는 경량 CNN 4종(MobileNetV3-Small, EfficientNet-B0, ResNet-18, ShuffleNetV2-x1.0)을 State Farm Distracted Driver 데이터셋에서 비교하였다. 실험 결과 ShuffleNetV2-x1.0이 1.26M 파라미터로 Top-1 89.18% 정확도를 달성하여 임베디드 환경에 가장 적합한 것으로 나타났다.

## Abstract

This paper compares four lightweight CNNs (MobileNetV3-Small, EfficientNet-B0, ResNet-18, ShuffleNetV2-x1.0) for a Driver Monitoring System (DMS) on the State Farm Distracted Driver dataset. ShuffleNetV2-x1.0 achieved 89.18% Top-1 accuracy with only 1.26 M parameters, showing the best fit for embedded deployment.

Key words
driver monitoring system, distracted driver, lightweight CNN

---

Ⅰ. 서  론

자율주행 Level 2~3 단계에서는 운전자의 부주의 행동을 실시간으로 감지하는 운전자 모니터링 시스템(DMS)이 필요하다[1]. 그러나 차량 임베디드 환경은 자원이 제한적이기 때문에 가벼운 모델을 사용해야 한다. 본 논문에서는 대표적인 경량 CNN 4종을 State Farm Distracted Driver 데이터셋[2]에서 비교하여 임베디드 환경에 적합한 모델을 찾고자 한다.

---

Ⅱ. 실험 방법

State Farm 데이터셋은 26명 운전자의 차내 영상 22,424장을 10개 행동 클래스로 라벨링한 데이터이다. 같은 운전자가 학습과 검증에 모두 포함되면 정확도가 과대평가되므로, 운전자 ID 기준 GroupKFold(k=5) 중 1개 fold(train 약 17.9k, val 약 4.5k)를 사용하였다.

비교한 모델은 MobileNetV3-Small, EfficientNet-B0, ResNet-18, ShuffleNetV2-x1.0의 4종이며, 모두 ImageNet 사전학습 가중치를 사용하고 마지막 분류기를 10-class로 교체하였다. 학습 설정은 입력 224×224, AdamW(lr=10⁻³), 배치 32, 30 epoch, CosineAnnealingLR을 동일하게 적용하였다. 평가는 Top-1 정확도, Macro F1, CPU/GPU 추론 지연시간(batch=1), 파라미터 수, FLOPs로 수행하였다.

---

Ⅲ. 실험 결과

ResNet-18은 Top-1 정확도 89.58%, Macro F1 88.88%로 가장 높은 정확도를 보였지만, 파라미터가 11.18M으로 가장 많고 CPU 지연시간도 34.7ms로 가장 느렸다. ShuffleNetV2-x1.0은 1.26M 파라미터와 5.1MB의 작은 모델 크기만으로 Top-1 89.18%, Macro F1 88.43%를 달성하여 ResNet-18과 정확도 차이가 0.4%p에 불과하였다. EfficientNet-B0는 4.02M 파라미터로 Top-1 87.88%를, MobileNetV3-Small은 1.53M 파라미터로 Top-1 84.62%를 기록하였다. MobileNetV3-Small은 CPU 지연시간이 10.0ms로 가장 빨랐지만 정확도가 가장 낮았다.

---

Ⅳ. 결  론

본 논문에서는 차량 임베디드 DMS에 사용할 경량 CNN 4종을 비교하였다. ShuffleNetV2-x1.0이 1.26M 파라미터와 5.1MB의 작은 모델 크기만으로 Top-1 89.18%를 달성하여 정확도와 효율 측면에서 가장 균형 잡힌 결과를 보였다. 향후에는 실제 차량 환경에서 촬영한 데이터로 추가 실험을 진행할 계획이다.

---

참 고 문 헌

[1] A. G. Howard et al., "Searching for MobileNetV3," *ICCV*, pp. 1314-1324, 2019.

[2] State Farm, "State Farm Distracted Driver Detection," Kaggle, 2016. [Online]. Available: https://www.kaggle.com/c/state-farm-distracted-driver-detection

[3] M. Tan and Q. Le, "EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks," *ICML*, vol. 36, pp. 6105-6114, 2019.

[4] K. He, X. Zhang, S. Ren, and J. Sun, "Deep Residual Learning for Image Recognition," *CVPR*, pp. 770-778, 2016.

[5] N. Ma, X. Zhang, H.-T. Zheng, and J. Sun, "ShuffleNet V2: Practical Guidelines for Efficient CNN Architecture Design," *ECCV*, pp. 116-131, 2018.
