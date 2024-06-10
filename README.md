# ECG-Myocardial-Infarction-Detection
## Overview:
1D-CNN을 이용하여 PTB-XL Dataset(심전도 데이터)로부터 심근경색류 질환을 진단하는 모델 제안 <br>

## Business Understanding
### 심전도(electrocardiogram, ECG)
ECG는 심장의 전기적 활동을 시간에 따라 기록한 그림이다. <br>

일반적으로 각 심장 박동 주기 내에서 P파, QRS 복합파, T파와 같은 주요 파형이 나타난다. [개념 공부한 것](https://kosonkh7.tistory.com/24)<br>

정상적인 심전도 신호는 일정한 주기와 반복적인 패턴을 가지지만, 그러나 비정상적인 심장 활동(예: 심근경색) 시에는 이러한 패턴에 변형이 발견 된다.<br>

ECG는 심장 상태를 평가하고, 부정맥, 심근경색, 전도 장애 등의 다양한 심장 질환을 진단하는 데 널리 사용된다.<br>

### 심근경색 (Myocardial Infarction, MI)
심근경색은 심장으로 가는 혈류가 차단되어 심장 근육이 손상하여 죽음을 유발하는 위험한 질환이다.<br>

가슴 통증, 호흡 곤란, 땀 흘림, 메스꺼움 등의 증상이 나타날 수 있다. 그러나 일부 환자는 무증상이기도 하기 때문에 정기적인 ECG 검사가 중요하다.<br>

심근경색은 즉각적인 치료가 이루어져야만 추가적인 심장 근육 손상을 막을 수 있기에, 조기 진단과 신속한 치료가 매우 중요하다. <br>

ECG는 이러한 상태를 빠르게 진단하는 데 중요한 역할을 한다. 심근경색 시 ECG에서 ST 분절 상승(STEMI), 비정상적인 Q파, T파 변화 등의 특징적인 변형이 발견되기 때문이다.<br>


### 1D CNN (Convolutional Neural Network)

1D-CNN은 1차원 시계열 데이터를 처리하는 데 특화된 구조로, ECG와 같은 신호 데이터 특징 추출에 적합한 구조이다.<br>

복잡한 시계열 패턴을 효과적으로 학습할 수 있어, 시간적 특징을 추출하는데 용이한 구조를 가지며,<br>

정상 심장 박동과 비정상 심장 박동(예: 부정맥)을 높은 정확도로 분류할 수 있다.<br>

1D-CNN은 비교적 적은 계산 비용을 요구하기 때문에 학습 및 추론 속도가 빠르다. 이는 실시간 ECG 모니터링 시스템에 적합하다.<br>

또한 상대적으로 적은 양의 데이터로도 좋은 성능을 발휘할 수 있다고 알려져 있기에, 의료 데이터에 적용하기 특히 유용하다.<br>

본 연구에서는 1D-CNN을 이용하여 심전도 데이터로부터 심근경색을 감지하는 모델을 제안한다.<br>


## Data Understanding

데이터셋 출처: https://physionet.org/content/ptb-xl/1.0.1/ <br>

데이터 상세 설명: https://www.nature.com/articles/s41597-020-0495-6 <br>

***

### 데이터셋 소개

- 공공 이용 가능한 데이터 

- 1989 년부터 1996 년까지 Schiller AG라는 ECG data 기록기를 통해 얻은 데이터

- 18885명의 환자로부터 21837 개 데이터 수집

- 10초간 측정 기록

- 12-lead ECG-waveform dataset

- 2명의 심장병 전문의가 레이블링함

- 500Hz (5000) / 100Hz (1000) 2가지 데이터 포함되어 있기 때문에 선택적으로 사용 가능

### 파일 구조 예시
ptbxl<br>
├── ptbxl_database.csv<br>
├── scp_statements.csv<br>
└── records100<br>
   ├── 00000<br>
   │   ├── 00001_lr.dat<br>
   │   ├── 00001_lr.hea<br>
   │   ├── ...<br>
   │   ├── 00999_lr.dat<br>
   │   └── 00999_lr.hea<br>
   ├── ...<br>
   └── 21000<br>
        ├── 21001_lr.dat<br>
        ├── 21001_lr.hea<br>
        ├── ...<br>
        ├── 21837_lr.dat<br>
        └── 21837_lr.hea<br>
          
### 레이블 정보        
각 데이터에 포함된 <scp_codes> 에 심장질환이 레이블링 되어있는데, 해당 질환의 확률이 딕셔너리 형태로 함께 제공된다. <br>

레이블 된 심장 질환은 5개의 주요 클래스와 24개의 하위 클래스로 구성되어 있는데, 아래 도표와 같다.<br>

![image](https://user-images.githubusercontent.com/83086978/168457272-1706181d-26cc-4634-a21b-3f6e041bd04c.png)

본 모델에서는 **MI(Myocardial Infarction)** 심근경색 클래스에 해당하는 하위 클래스 진단 확률이 100인 데이터를 Target Label으로 설정하였다.<br>

### ECG 데이터 시각화
![image](https://user-images.githubusercontent.com/83086978/168457354-f9ea4e0a-1fe5-4e7e-b7d6-c406ac44a64c.png)

## Modeling and Evaluation

![image](https://github.com/kosonkh7/ECG-Myocardial-Infarction-Detection/assets/83086978/5d3739f2-6499-4ace-b18b-9454d28e33d3)

5개의 1D CNN Block과 2개의 Fully Connected Layer로 설계하였다.<br>

각 블럭은 실험적으로 좋은 성능을 보이는 구성 요소를 채택하였다.

학습 : 검증 : 테스트 = 7 : 2 : 1 비율로 데이터를 나누었다.<br>

![image](https://github.com/kosonkh7/ECG-Myocardial-Infarction-Detection/assets/83086978/f424f974-4ddc-4f5f-88c9-2a6011da56d3)

학습은 200 에포크 진행하였고, 조기종료 조건을 설정하였다.<br>

val_loss 기준 90 에포크부터 과대적합이 진행되는 것을 확인할 수 있었고,<br>

학습 결과 테스트셋 기준으로 약 91%의 정확도를 기록하였다.

test_acc: 0.9096686244010925 <br>
test_loss: 0.20646625757217407 <br>

표면적으로 테스트셋 대상으로도 높은 정확도를 보이고 있지만,<br>

심근경색은 빠르고 정확한 진단이 매우 중요한 질환이기 때문에, 100%에 근사한 정확도를 보이는 모델을 개발하는 것이 앞으로의 과제이다.<br>

또한 모델링 과정에서 실험적으로 하이퍼파라미터의 설정을 바꿔가며 분류 성능을 평가하였는데,<br>

Optuna와 같은 자동 하이퍼파라미터 최적화 프레임워크를 적용할 수 있는 형식으로 코드를 설계했다면 <br>

보다 많은 실험을 통해 더 높은 정확도를 보이는 모델을 개발할 수 있었을 것이라고 생각한다. <br>
