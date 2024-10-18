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

- 평균 Signal rate = Bit rate / 3 = Bandwidth (c = 1 / 3, r = 1)

## Block Coding
- Block Coding은 동기화나 오류 검출에 특화된 방법
- 여분의 정보(redundant bit)를 데이터에 포함하여 동기화나 오류 검출

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKIDzL%2Fbtr72ZmYWR2%2FUTTQzo1Zev74C9lLvHE9R1%2Fimg.png">

- mB / nB coding은 m bit로 이루어진 데이터를 n bit로 변환, 기존 m개의 bit에 여분의 비트를 더했기 때문에 항상 (n > m)

### 4B / 5B
- 4bit의 데이터를 보낼 때 NRZ-I Line coding을 사용하는 경우 나타나는 문제점을 해결하기 위해 사용
    - NRZ-I의 문제 : 연속된 1은 DC 성분 제거가 가능했지만 연속된 0은 전압을 바꾸지 않기 때문에 DC 성분이 그대로 존재
    - 4bit로 된 데이터를 5bit로 다시 표현하여 해결
    <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fsv2W3%2Fbtr73yvH3ha%2FEO6NPgAqFL69eDgcwV5moK%2Fimg.png">

## Scrambling
- AMI encoding은 BW가 낮고 DC 성분이 존재하지 않지만 동기화 문제가 남아있음
- AMI encoding의 연속된 0으로 생기는 동기화 문제를 해결하기 위해 사용
- 주로 장거리 통신에 사용됨
- Design Goal
    - No DC Components
    - No long sequences of zero level line signal
    - No reduction in data rate
    - error detection capability

### B8ZS
- Bipolar with 8 Zero Substitution
- 8개의 연속된 0을 000VB0VB 신호로 대체

 <p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Feb1f778a-adf4-43ed-bd26-24e38f28ebc5%2Fimage.png">

 ### HDB3
 - High-Density Bipolar 3-zero
 - 4개의 연속된 0을 대체
    - 0이 아닌 펄스의 개수가 홀수면 000V로 대체
    - 0이 아닌 펄스의 개수가 짝수면 B00V로 대체

 <p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Fb53c8269-9a04-4b68-bf50-d03f0659ac07%2Fimage.png">


# 4.2 Analog-to-Digital Conversion
## PCM
- Pulse Code Modulation
- Analog signal을 Digital data로 변환하는 방법

 <p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYWifq%2Fbtr77P3VGtA%2FcYckDJFKvHqTjg04Ce3sb0%2Fimg.png">

### Step 1 : Sampling
- 일정한 간격으로 신호의 진폭 구하기
- PAM : Pulse amplitude modulation

<p align="center"><img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Fdatacommandnet.blogspot.com%2Fp%2Fanalog-to-digital-conversion.html&psig=AOvVaw0FLfZjhc1mVjHNMmfcYG0o&ust=1729355458729000&source=images&cd=vfe&opi=89978449&ved=0CBQQjRxqFwoTCJD2z6OtmIkDFQAAAAAdAAAAABAJ">

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZVPbe%2Fbtr726M0yX2%2FBMTAyY1XuHkrCA3QDY2XtK%2Fimg.png">

- 위의 그림에서 +값은 0 ~ 4단계를 거치고 -값은 -4 ~ 0단계를 거침
- -4~4 사이의 값을 갖도록 정규화(Normalization), 값을 5로 나눔

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuPzxE%2Fbtr724PcCZc%2FG0klwKpcSCkw01IDN67CTk%2Fimg.png">

- Normalized PAM values는 sampling한 값들을 정규화했다는 의미

#### Sampling Rate
- Nyquist rate
- sampling rate는 최대 Bandwidth의 최소 2배가 되어야 함

<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Fec588cbe-55e7-4aa4-b5f8-2d73f1c46668%2Fimage.png">

### Step 2 : Quantizing
- 양자화 : 연속적인 Analog 값을 이산적인 Digital로 변환

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fusgwo%2Fbtr726faQEY%2FF0wTloOQyHimsx1YBhuFH1%2Fimg.png">

- Quantization Code
    - Quantization Level을 정하여 -4 ~ 4단계를 0 ~ L-1로 표현
    - L이 낮으면 신호의 변동이 많을 경우 Quantization Error 증가

- Quantization Error
    - SNR db = 6.02 * nb + 1.76 (dB)
    - nb : bits per sample, log2L
    - ex) Quantization Level = 8, nb = 3

### Step 3 : Encoding

<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2F4a706aba-b66c-41bd-9804-6bab1bcdec59%2Fimage.png">

- Quantization code를 2진수로 변환
- Bit rate = sampling rate * number of bits per sample
           = fs * nb
           = 2 * BW * nb

## DM
- Delta Modulation

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLcboO%2Fbtr73oNyqR3%2FV9mnqkILlYKehA4K5xoIr1%2Fimg.png">


- Analog signal을 PAM 과정을 거쳐 digital data로 Encoding
- Encoding 한 Digital data를 Line Coding하여 Digital signal로 변환

# 4.3 Transmission Modes

<p align="center"><img src="https://prodiffs.com/storage/img/images_1/difference-between-synchronous-and-asynchronous-transmission_2.jpg">

