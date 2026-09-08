# insurance_premium_prediction
## 프로젝트 주제 : 신규 보험 가입 고객 유치를 위한 예상 보험료 측정 진단  
## 프로젝트 기한 2024.3 ~ 2024.6
## 분석 방법
### data 구성 확인
'Medical Cost Personal Datasets'  
-> Brett Lants가 쓴 'Machine Learning with R'에서 제공하는 insurance data  
-age, sex, bmi, children, smoker, region, charges 7가지 칼럼으로 구성  
<img width="1127" height="187" alt="image" src="https://github.com/user-attachments/assets/9c33774d-cf09-4706-9871-d760df51b61c" />
-dataset의 값 개수(count), mean, 표준편차(std), minimun, maximun, 백분위수 한눈에 보기  
<img width="413" height="264" alt="image" src="https://github.com/user-attachments/assets/5d266339-b0de-46ef-895a-00946ccbbf83" />
### data 전처리 및 시각화
#### data 전처리
-1개의 invalid value 제거  
-missing value 존재하지 않음  
-bmi, charges 칼럼에서 standard scalar 이용하여 outlier 찾아 제거
#### data 시각화
-categorical variables(sex, smoker, region)시각화  
-quantative variables(children, age, bmi, charges)시각화 
-charges(target variable) 중심의 데이터 연관성 분석  
-numerical columns 간 연관성  
  numerical columns 중에는 age(0.3), bmi(0.2)가 charges와 연관성이 높은 편이다.
  categorical columns는 레이블 인코딩(string>float 변환)을 하더라도 연관성을 계산하기는 어렵다.  
### label encoding
-sex : female(0), male(1)  
-smoker : n0(0), yes(1)
-region : northeast(0), northwest(1), southeast(2), southwest(3)  
-label : High(0), Low(1)
### data split
-data 칼럼 나누기(원인-결과)  
  원인 : 'sex', 'smoker', 'region', 'age', 'bmi', 'children'  
  결과 : 'charges'
-split data (train : test = 0.8 : 0.2)
-results :  
Training set : 1069  
Test set : 268  
Trainig target variable: : 1069  
Testing target variable : 268  
### 모델 학습-진료비 예측
<img width="1093" height="419" alt="image" src="https://github.com/user-attachments/assets/6c4942f0-127a-4e04-8217-3af6442528e0" />
<img width="1097" height="413" alt="image" src="https://github.com/user-attachments/assets/6878cc8d-0798-41ed-aaff-ec8e36b6ac7a" />
<img width="1098" height="409" alt="image" src="https://github.com/user-attachments/assets/b030916b-d518-4dd3-abea-811122ead18b" />
### 모델 평가
<img width="959" height="405" alt="image" src="https://github.com/user-attachments/assets/3d142e6a-b213-43e4-aa59-1379e0d4effe" />
### 결과 확인
-가장 성능이 좋은 Gradient Boosting을 선택 후 feature importance 확인  
smoker: 0.6709143170466134  
bmi: 0.188440959726968  
age: 0.12287076244893755  
children: 0.012763821714206796  
region: 0.003859842101419106  
sex: 0.001150296961855103  
-전체 데이터셋에 대해 예측 수행  
<img width="738" height="342" alt="image" src="https://github.com/user-attachments/assets/b2b28676-ce2b-418f-8d36-7bb6f725485d" />
### classification 기준 설정
-charges 칼럼을 High/Low로 분할  
charges 칼럼을 변화율이 가장 큰 구간을 기준으로 'High'&'Low'label로 나눈다.  
Low charges 965, High charges 137로 약 9 : 1의 비율로 데이터가 나뉜다.  
<img width="1878" height="695" alt="image" src="https://github.com/user-attachments/assets/4bce6c2a-8bc2-4598-991b-e6e760eaca85" />
### data split
-data 칼럼 나누기(원인-결과)  
  원인 : 'sex', 'smoker', 'region', 'age', 'bmi', 'children'  
  결과 : 'label'
-split data (train : test = 0.8 : 0.2)
-results :  
Training set : 953  
Test set : 239  
Trainig target variable: : 953  
Testing target variable : 239  
### 모델 학습 및 평가-High/Low classification
<img width="988" height="399" alt="image" src="https://github.com/user-attachments/assets/4a134be6-0ab0-4cc7-b5bb-4669f8ae1b4e" />
### 결과 확인
-가장 성능이 좋은 Random Forest를 선택 후 feature importance 확인  
smoker: 0.4829974565260843  
bmi: 0.21519401748621855  
age: 0.1836707425364386  
children: 0.06010553360356189  
region: 0.03812158569489455  
sex: 0.019910664152802182  
-전체 데이터셋에 대해 예측 수행  
<img width="807" height="346" alt="image" src="https://github.com/user-attachments/assets/053754bb-e46d-4547-a84b-bf2cc594e2f9" />
### 최종 결론
<img width="883" height="284" alt="image" src="https://github.com/user-attachments/assets/70d5204e-c550-40bb-a499-c8c70d0e65f8" />
