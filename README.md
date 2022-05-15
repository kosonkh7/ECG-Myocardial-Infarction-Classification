# ECG-Myocardial-Infarction-Detection
PTB-XL Dataset(심전도 데이터)를 활용한 1D-CNN 기반 심근경색 감지 모델입니다. <br>

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




