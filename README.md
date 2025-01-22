# 프로젝트 개요
본 프로젝트는 온도에 영향을 받는 설비들을 위해 날씨의 변화에 따라 공장 내부 온도를 예측하는 모델을 구현하는 프로젝트입니다. 

데이터는 기상청Open API - 지상관측 - 종관지상관측에서 가져왔습니다.https://apihub.kma.go.kr 

실험을 하기 위해 총 6개의 모델(ARIMA, Auto-ARIMA, SARIMA, Prophet, RandomForest, RandomForest with Recursive Multi-step Forecast)을 사용했고, 여러가지 방식을 적용한 모델도 있습니다. 자세한 사항은 코드를 참조하십시오.

# 실험 결과
시계열 데이터인 점을 고려하고, 모델이 올라갈 환경이 저사양인 점을 고려하여 먼저 통계적 기법의 모델을 적용해보았습니다.
- ARIMA ```(MAE = 2.06083333333333355, Running Time = 41s)```
- Auto-ARIAMA ```(MAE = 2.060875, Running Time = 1m)```
- SARIMA ```(MAE = 0.8157374642044267, Running Time = 1m)```
- Prophet ```(MAE = 0.43402921414353085, Running Time = 20s)```
- Prophet with Exogenous variable ```(MAE = 0.43402921414353085, Running Time = 24s)```
- RandomForest Linear Regressor ```(MAE = 0.882211812754272, Running Time = 16s)```
- RandomForest with recursive multi-step forecast ```(MAE = 1.2354693559411987, Running Time = 25s)```
- RandomForest with Exogenous variable and recursive multi-step forecast ```(MAE = 0.5320561967060167, Running Time = 26s)```

이 중 어느 시점을 예측하던 정확도의 편차가 크지 않았던 것은 마지막 모델입니다. (랜덤포레스트를 Recursive Multi-step방식으로 예측하도록하고 날씨 온도와 현장 온도 모두를 독립변수로 두지 않고 날씨온도를 외생변수로 취급한 모델)

# 문제해결
시계열 데이터를 다루는 것도, 통계적 기법 모델을 다루는 것도 모든게 처음이였습니다. 그래서 단계별로 문제를 해결하기 위해 문제정의, 데이터분석, 모델서칭, 모델실험, 결과분석의 과정을 설정했고 이 과정을 하나씩 수행해가며 선형적으로 문제를 풀어갔습니다. 처음에 정해두었던 프로세스 덕분에 처음 보는 문제를 혼자서 능동적으로 풀 수 있었습니다. 

# 성과
- 프로그램이 저사양PC의 백그라운드에서 낮은 CPU사용률과 낮은 메모리 사용률을 가지고 동작할 수 있도록 구현했습니다.
- 허용되는 오차범위 내에서 성공적으로 예측하는 모델을 완성시켜 기업에 기술이전 했습니다.

# 배운 점
- 통계적 분석은 데이터간의 인과관계를 밝혀내려고하고 특정 가정의 존재를 전제로 진행한다면, 머신러닝은 데이터의 분포나 가정에 크게 의존하지 않고 데이터가 가지는 특징(Feature)을 그대로 학습합니다.
- 머신러닝이 시계열 데이터를 다루는 방식 중 하나인 Recursive Multi-step Forecast 방식에 대해서 알게되었습니다.
