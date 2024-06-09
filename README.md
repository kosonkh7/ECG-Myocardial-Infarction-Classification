# ECG-Myocardial-Infarction-Detection
## Overview:
PTB-XL Dataset(심전도 데이터)를 이용하여 심근경색류 질환의 특징을 추출하는 1D-CNN 기반 분류 모델 설계 <br>

## Business Understanding
### 심전도
심전도(electrocardiogram, ECG)는 심장의 전기적 활동을 시간에 따라 기록한 그림이다. <br>

일반적으로 각 심장 박동 주기 내에서 P파, QRS 복합파, T파와 같은 주요 파형이 나타난다. [개념 공부한 것](https://kosonkh7.tistory.com/24)<br>

정상적인 심전도 신호는 일정한 주기와 반복적인 패턴을 가지지만, 그러나 비정상적인 심장 활동(예: 심근경색) 시에는 이러한 패턴에 변형이 발견 된다.<br>

ECG는 심장 상태를 평가하고, 부정맥, 심근경색, 전도 장애 등의 다양한 심장 질환을 진단하는 데 널리 사용된다.<br>

### 심근경색
심근경색(Myocardial Infarction, MI)은 심장으로 가는 혈류가 차단되어 심장 근육이 손상하여 죽음을 유발하는 위험한 질환이다.<br>

가슴 통증, 호흡 곤란, 땀 흘림, 메스꺼움 등의 증상이 나타날 수 있다. 그러나 일부 환자는 무증상이기도 하기 때문에 정기적인 ECG 검사가 중요하다.<br>

심근경색은 즉각적인 치료가 이루어져야만 추가적인 심장 근육 손상을 막을 수 있기에, 조기 진단과 신속한 치료가 매우 중요하다. <br>

ECG는 이러한 상태를 빠르게 진단하는 데 중요한 역할을 한다. 심근경색 시 ECG에서 ST 분절 상승(STEMI), 비정상적인 Q파, T파 변화 등의 특징적인 변형이 발견되기 때문이다.<br>


### 1D CNN

1D-CNN(Convolutional Neural Network)은 시간적 특징을 추출하는데 용이한 구조를 가지고, 비교적 적은 계산 비용을 요구하기에, 심전도와 같은 신호 데이터 분류 연구에 널리 쓰입니다.<br>

본 연구에서는 1D-CNN을 이용하여 심전도 데이터로부터 심근경색을 감지하는 모델을 제안합니다.<br>

데이터셋 출처: https://physionet.org/content/ptb-xl/1.0.1/ <br>

데이터 상세 설명: https://www.nature.com/articles/s41597-020-0495-6 <br>

***

## 데이터셋 소개

- 공공 이용 가능한 데이터 

- 1989 년부터 1996 년까지 Schiller AG라는 ECG data 기록기를 통해 얻은 데이터

- 18885명의 환자로부터 21837 개 데이터 수집

- 10초간 측정 기록

- 12-lead ECG-waveform dataset

- 2명의 심장병 전문의가 레이블링함

- 500Hz (5000) / 100Hz (1000) 2가지 데이터 포함되어 있기 때문에 선택적으로 사용 가능

## 파일 구조 
ptbxl<br>
├── ptbxl_database.csv<br>
├── scp_statements.csv<br>
├── records100<br>
│   ├── 00000<br>
│   │   ├── 00001_lr.dat<br>
│   │   ├── 00001_lr.hea<br>
│   │   ├── ...<br>
│   │   ├── 00999_lr.dat<br>
│   │   └── 00999_lr.hea<br>
│   ├── ...<br>
│   └── 21000<br>
│        ├── 21001_lr.dat<br>
│        ├── 21001_lr.hea<br>
│        ├── ...<br>
│        ├── 21837_lr.dat<br>
│        └── 21837_lr.hea<br>
└── records500<br>
   ├── 00000<br>
   │     ├── 00001_hr.dat<br>
   │     ├── 00001_hr.hea<br>
   │     ├── ...<br>
   │     ├── 00999_hr.dat<br>
   │     └── 00999_hr.hea<br>
   ├── ...<br>
   └── 21000<br>
          ├── 21001_hr.dat<br>
          ├── 21001_hr.hea<br>
          ├── ...<br>
          ├── 21837_hr.dat<br>
          └── 21837_hr.hea<br>
          
## 레이블 정보        
각 데이터에 포함된 <scp_codes> 에 심장질환이 레이블링 되어있는데, 해당 질환의 확률이 딕셔너리 형태로 함께 제공됩니다. <br>

레이블 심장 질환은 5개의 주요 클래스와 24개의 하위 클래스로 구성되어 있는데, 아래 도표와 같습니다.<br>

![image](https://user-images.githubusercontent.com/83086978/168457272-1706181d-26cc-4634-a21b-3f6e041bd04c.png)

본 모델에서는 **MI(Myocardial Infarction)** 심근경색 클래스에 해당하는 하위 클래스 진단 확률이 100 값을 가지면 Target Label으로 설정하였습니다.<br>

## ECG 데이터 시각화
![image](https://user-images.githubusercontent.com/83086978/168457354-f9ea4e0a-1fe5-4e7e-b7d6-c406ac44a64c.png)




