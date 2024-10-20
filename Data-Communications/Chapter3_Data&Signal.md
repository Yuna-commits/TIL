# 3.1 Analog and Digital
- Data
    - analog data : continuous
    - digital data : discrete
    
- Signal
  
<img width="400" height="200" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbeYK9y%2Fbtr9BHqgvEm%2Frjf9creJAWAP198lji8aGk%2Fimg.png">
<img width="400" height="200" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FchjefS%2Fbtr9z8B94Z2%2Fzu7Bhck0LCk33EUxHVqLu1%2Fimg.png">

  - analog signal
      - infinite nuber of values
  - digital signal
      - limited number of values

- Signal : Periodic / Nonperiodic
  - periodic : 신호에 패턴이 존재
  - period(T) : 패턴이 나타나는 주기
  - cycle : 하나의 완벽한 패턴
  - 주로 periodic analog signal, nonperiodic digital signal을 사용

# 3.2 Periodic Analog Signal
- analog signal이 주기적이면 simple signal과 composite signal로 나눌 수 있음
  - simple signal : sine wave, 더이상 분해할 수 없음
  - composite signal : 여러 개의 sine wave로 분해할 수 있음

## Feature of analog signal
1. Amplitude(진폭)

<img width="600" height="400" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkAIcj%2Fbtr9AtMSSRj%2F6GnlrzL9kuR4vHbk8mKrZ1%2Fimg.png">

- peak amplitude는 sine wave에서 전압이 가장 클 때를 의미

2. Frequency(주파수, 진동수)

<img width="600" height="400" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FciIruD%2Fbtr9sf20sf2%2F4tDKQznaoldkgwz5fkO8Ak%2Fimg.png">

- 1초에 나타난 cycle의 개수
- 위 그림은 1초에 12번의 cycle이 돌아감 -> frequency 12 Hz
- Period(주기)는 frequency의 역수, 12 Hz -> period 1 / 12 s
- Period 증가 -> Frequency 감소 <=> Period 감소 -> Frequency 증가
- High Frequency : 짧은 시간동안의 변화
- Low Frequency : 긴 시간동안의 변화

### Frequency 0, Infinite
- frequency는 1초에 몇 번의 패턴, 즉 신호의 변화가 몇 번 있었는지를 나타냄
- 따라서 정해진 시간동안 신호에 변화가 없었다면(period가 엄청나게 긴 경우) frequency = 0에 수렴
- 신호가 갑작스럽게 변한다면(period가 엄청나게 짧은 경우) frequency = infinite으로 발산
- digital signal 형태에서 수직부분은 frequency = infinite, 수평부분은 frequency = 0

3. Phase(위상)

<img width="600" height="400" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsO7HJ%2Fbtr9MoLaGFJ%2FPaqnI4CPM9IKVHzxqSkWl1%2Fimg.png">

- 기본 sine wave형태에서 x축으로의 이동 정도
- s(t) = A * sin(2π * f * t + Φ)
- Φ : phase, 0보다 커지면 sine wave가 왼쪽으로 이동, 0보다 작아지면 오른쪽으로 이동

##
