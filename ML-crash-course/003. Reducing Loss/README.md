# 손실 줄이기 : 반복 방식(An Iterative Approach)
반복 학습 : 임의의 지점에서 시작 -> 손실 계산 -> 다른 값을 추정 -> 시행착오 반복해서 최적 모델을 찾음

가중치, 편향에 대한 초기 예측 값 -> 예상 손실 값이 가장 적은 가중치와 편향을 학습할 때까지 예상 값 조정

- 대규모 데이터 세트에 적용 용이
- 머신러닝에서 널리 사용됨

## 반복 방식의 모델 학습

1. 하나의 특성 x1을 가지고 하나의 예측 y를 반환하는 모델

```python
y = b + w1(x1)
```

2. `b`, `w1` 초깃값 설정

```python
b = 0
w1 = 0
```

위와 같은 설정을 사용 (선형 회귀 문제에서는 초깃값이 별로 중요하지 않음)

3. 최초 특성 값 입력

```python
x1 = 0
```

위와 같이 최초 특성 값이 10이라고 가정

```python
y = 0 + 0(10)
y = 0
```

4. 손실 계산

- 제곱 손실 함수를 사용한다고 가정
- 손실 함수는 두 개의 입력 값을 취함(모델의 예측 값, 올바른 라벨)

5. 매개변수 업데이트 계산

- ML 시스템은 손실함수의 값을 검토하여 `b`, `w1`의 새로운 값을 생성
- 손실 값이 가장 낮은 모델 매개변수를 발견할 때까지 반복 학습

## 수렴
전체 손실이 변하지 않거나 매우 느리게 변할 때까지 반복 -> 모델이 수렴

# 손실 줄이기 : 경사하강법(Gradient Descent)

매개변수 업데이트 계산 과정의 실질적인 알고리즘

회귀 문제에서는 볼록 함수 모양의 손실 대 가중치 도표가 산출됨(기울기가 정확하게 0인 지점인 최솟값이 하나만 존재 -> 이 지점에서 손실 함수가 수렴)

## 경사하강법
모든 `w1` 값의 손실 함수를 계산하는 것은 비효율적 -> 더 나은 방법? 경사하강법

1. `w1`에 대한 시작점을 선택(중요 x -> 보통 0 또는 임의의 값을 선택)

2. 시작점에서 손실 곡선의 기울기(= 미분 값)를 계산

> ### 기울기
> - 편미분의 벡터 -> 어느 방향이 정확한지 알려줌
> - 특성 : 방향, 크기
> - 손실 함수 값이 가장 크게 증가하는 방향을 향함

3. 가능한 빨리 손실 줄이기 위해 기울기의 반대 방향으로 이동

3. 손실 함수 곡선의 다음 지점을 결정 : 기울기 크기의 일부를 시작점에 더함

4. 기울기 보폭을 통해 다음 지점으로 이동 -> 반복해 최소값에 접근

# 손실 줄이기 : 학습률(Learning Rate)

- 경사하강법 : 기울기에 학습률(보폭) 스칼라를 곱하여 다음 지점을 결정

- 초매개변수 : 프로그래머가 ML 알고리즘에서 조정하는 값

## 학습률
- 학습률이 너무 작으면 학습 시간이 오래 걸림
- 학습률이 너무 크면 곡선의 최저점을 무질서하게 이탈할 수 있음

## 골디락스 학습률
이상적인 학습률

- 손실 함수가 얼마나 평탄한지 여부와 관련
- 기울기가 작다면 더 큰 학습률을 시도 -> 작은 기울기 보완, 더 큰 보폭

# 손실 줄이기 : 확률적 경사하강법(Stochastic Gradient Descent)

## 배치
단일 반복에서 기울기를 계산하는 데 사용하는 예의 총 개수

- 배치가 너무 커지면 단일 반복으로도 계산하는 데 오랜 시간이 걸릴 수 있음
- 배치 크기가 커지면 중복의 가능성도 높아짐
- 예를 무작위로 선택하면 훨씬 적은 데이터셋으로 중요한 평균값을 구할 수 있음

## 확률적 경사하강법(SGD)
반복당 하나의 예(배치크기 1)를 사용

- 확률적 : 하나의 예를 무작위로 선택
- 반복이 충분하면 효과는 있으나 노이즈가 심함

## 미니 배치 확률적 경사하강법(미니 배치 SGD)
전체 배치 반복 & SGD 절충안

- 미니 배치 : 무작위로 선택한 10~1000개 사이의 예로 구성
- SGD의 노이즈를 줄이면서도 전체 배치보다 효율적