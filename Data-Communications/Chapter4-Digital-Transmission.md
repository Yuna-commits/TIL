# How to convert data into signal?
- Encoding
    - digital/analog "data"를 digital signal로 변환하는 방법
    - 변환된 digital signal을 data로 다시 바꾸는 것은 Decoding이라고 함

- Modulation
    - encoding된 data를 "carrier signal"을 이용하여 analog signal로 변환하는 방법
    - source data에 따라 carrier signal의 특성을 변환

# 4.1 Digital-to-Digital Conversion
- Data element vs Signal element

    <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdaexNC%2Fbtr7LrKUN9q%2FkqIaH8jEM8wRwrW6tJryxk%2Fimg.png">

    - r = data elements/signal elements
    - 몇 개의 data를 몇 개의 signal로 보낼 수 있는가?/표현할 수 있는가?
    - data element는 우리가 보내고 싶은 것, signal element는 우리가 보낼 수 있는 것의 차이

- Data rate vs Signal rate
    - Data rate은 1초당 보낼 수 있는 bit(data element)의 개수, 단위 bps
    - Signal rate은 1초당 보낼 수 있는 signal element의 개수, 단위 baud
    - Signal rate = c * Data rate * (1 / r)(baud)
        - r = log2L, Signal rate = Bit rate / log2L (c=1)로도 표현
        - Bit rate = Signal rate * log2L
    - Data rate를 높이고 Signal rate를 낮추는 것이 중요!
        - Data rate는 신호의 전달 속도를 높이면 증가, Signal rate는 Bandwidth을 낮추면 감소
    - 최소 Bandwidth Min.BW = S = N / r

## Line Coding
- digital data를 digital signal로 변환
### Line Coding 주의할 요소
1. Baseline Wandering
    - digital signal을 다시 data로 변환할 때 수신된 signal power의 평균을 계산하는데 이 평균이 baseline
    - 수신된 signal power는 baseline에 대해 평가되어 decoing할 때 데이터 값이 결정됨
    - 그런데 baseline 값은 연속된 0, 1이 들어올 때 갑자기 바뀔 수 있음(baseline wandering)
        - ex) baseline = 0.01W, 연속된 0(data = 0)이 수신되다가 0.012W가 수신될 경우 signal > baseline, 미세한 차이로도 data = 1로 디코딩 될 수 있음

2. DC Components
    - DC(Direct Current), 직류 성분은 값이 변하지 않기 때문에 frequency = 0
    - 연속된 0, 1을 받는 쪽에서 문제가 발생
        - data = 1을 보냈음에도 frequency가 0이기 때문에 아무 소리도 안들릴 수 있음
    - 따라서 이런 연속적인 데이터의 흐름을 연속적이지 않게 encoding해야 함
    - 평균 Amplitude = 0이면 DC성분이 없고, 0이 아니면 DC성분이 있음

3. Self-Synchronization

    <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcyOoY4%2Fbtr7RrvVUaY%2FpR0ok4fuMgWpmjs4ZKwN50%2Fimg.png">

    - Self-Synchronization(동기화)은 신호가 지연되는 경우에 필요한 요소
    - 수신측은 송신측과 반드시 정확한 타이밍에 bit를 받아야 함
    - 데이터의 시작, 중간, 끝을 표시하여 전송하는 것으로 해결 가능

### Line Coding의 종류

    <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYFs7M%2Fbtr7R41G87y%2F3Iw4kFkHONMeaOUecZPXoK%2Fimg.png">

#### Unipolar : NRZ
- Non-Return-to-Zero
- Unipolar : uses only one voltage level
    - 1 -> +, 0 -> 0으로 표현

<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Fae2a1ed3-e8d5-47cd-b2cb-15b480e848b6%2Fimage.png">

- 하나의 데이터를 표현하기 위해 중간에 전압 변화를 주지 않음
- 자원도 많이 들고 DC 성분, 동기화 문제도 해결 x

### Polar :  NRZ
- Polar : +/-전압 두가지 사용

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbkAYe1%2Fbtr7PiGd5xt%2F2I6PuOXGcXTfztRaZuFEJK%2Fimg.png">

- NRZ-L(Level)은 0일 때 +, 1일 때 -전압 사용
- NRZ-I(Invert)는 0일 때는 전압의 변화가 없고 1일 때는 전압을 변화시킴
    - 연속된 1이 올 경우에는 DC 성분을 제거할 수 있음, 0일 때는 x
- Self-synchronization x
- r = 1, 평균 Signal rate = Bit rate / 2 = Bandwidth

### Polar : RZ
- Return-to-Zero
- 두 개의 전압으로 데이터를 표현하는데 중간에 0을 거쳐가는 방식

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FctJEgf%2Fbtr7R2XaMUl%2FB5D1MK8NWSBn475SDhv2Qk%2Fimg.png">

- 1일 때는 + -> 0, 0일 때는 - -> 0
- 연속된 데이터가 들어와도 구분할 수 있기 때문에 DC 성분 제거
- 중간에 0을 거쳐가며 동기화 수행 가능, Self-synchronization 만족
- 단점은 데이터 하나를 표현하기 위해 두 번의 신호를 보내야 함, 더 많은 Bandwidth 필요
- r = 1 / 2, 평균 Signal rate = Bit rate = Bandwidth

### Polar : Bipahse : Manchester
- RZ + NRZ-L

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb38kal%2Fbtr7OKiF75z%2Fc5Q1CxS4tkaqW0NcZkIzck%2Fimg.png">

- 1일 때는 - -> +, 0일 때는 + -> -
- 중간에 0을 거치지는 않지만 비트와 비트 사이에서 일어나는 전압 변화로 동기화 수행 가능
- DC 성분도 제거
- r = 1 / 2, 평균 Signal rate = Bit rate = Bandwidth

### Polar : Bipahse : Differential Manchester

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCOOIX%2Fbtr7Hh2zcj5%2F4pgnuKDkVWd4ouWrYBQ2D1%2Fimg.png">
<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbI43HR%2Fbtr7OKJMkEH%2FCw7HvhUJaxuSjUK7D3mjK1%2Fimg.png">

- 다음 비트가 1이면 전압 변화를 주고 0이면 변화를 주지 않음

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FD2NXH%2FbtscfBmQyFh%2Fl1kSQ9e17z2AWHiUCSWuCk%2Fimg.png">

- 0으로 시작하는 부분에선 inversion이 먼저 일어남

### Bipolar : AMI, Pseudoternary
- Bipolar는 +, - 0으로 데이터 처리, 1 data <-> 1 signal

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdQO2KV%2Fbtr7PqxibFE%2FtWYhVup8W081uJP8old6lk%2Fimg.png">

- AMI는 0일때 0, 1일 때는 +, -의 전압을 번갈아 사용
- Pseudoternary는 1일 때 0, 0일 때 +, -의 전압을 번갈아 사용
- 평균 전압이 0V로 DC 성분 x, 동기화도 x
- r = 1, 평균 Signal rate = Bit rate / 2 = Bandwidth

### Bipolar : Multilevel Schemes
- mBnL Coding
    - m : 2진수 패턴 길이, B : 2진수, n : 신호 패턴 길이, L : signal level 개수
    - L = 2 -> B(Binary)
    - L = 3 -> T(Tenary)
    - L = 4 -> Q(Quaternary)
    - m개의 data 패턴이 n개의 signal 패턴으로 표현됨

1. 2B1Q
- 2 Binary 1 Quaternary
- 하나의 signal이 2개의 data(bit)를 받고 4개의 서로 다른 전압을 사용
- 평균 Signal rate = Bit rate / 4 = Bandwidth (c = 1 / 4, r = 1 / 2)

<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2F72a81a58-5ef3-42e0-a1f0-52797e4c6152%2Fimage.png">

2. 8B6T
- 8 Binary 6 Ternary
- 8 bit를 길이 6인 signal로 표현, 3개의 서로 다른 전압 사용
- 평균 Signal rate = 3 * Bit rate / 4 = Bandwidth (c = 1 / 2, r = 8 / 6)

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxvzfB%2Fbtr7XdyrM2k%2FQ0SuctQHJPV4KKmKvD0tyk%2Fimg.png">

- 8B6T는 데이터의 평균 진폭이 항상 0이 되도록 맞춤
    - -0-0++, -+-++0, +--+0+를 보낼 때 평균 진폭을 0으로 맞추기 위해 마지막 데이터는 inversion하여 -++-0-로 바꿈
    - DC 성분 x
- 2^8 = 256개 데이터 패턴, 3^6 = 729개 전압 패턴
    - 사용하지 않은 나머지 패턴은 오류 검출이나 동기화에 사용

### Multi-transition : MLT-3
- +, -, 0 사용
- 규칙
    1. 다음 비트가 0이면 전압을 변화시키지 않음
    2. 다음 비트가 1인데 현재 전압이 0이 아니면 다음 전압은 0
    3. 다음 비트가 1인데 현재 전압이 0이면 다음 전압은 가장 최근에 보낸 0이 아닌 신호의 반대 전압을 사용

    <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZRYyC%2Fbtr7StWeBSt%2FTkKegR3r1xLxCThVhCK5j0%2Fimg.png">

