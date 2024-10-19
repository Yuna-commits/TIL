# 5.1 Digital-to-Analog Conversion
- [Chapter4 Review](https://github.com/Yuna-commits/TIL/blob/main/Data-Communications/Chapter4_Digital-Transmission.md)
  - digital data를 analog signal로 전송하기 위해 필요한 Bandwidth은 Signal rate에 비례
  - signal rate : 1초에 보낼 수 있는 signal의 개수
 
## Carrier Signal
  - analog signal을 기반으로 정보를 전달하는 signal

## Modulation, Demodulation

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWGoEl%2Fbtr9nJPvUWp%2FNTMx1wkvCpkdZB65KxT4T1%2Fimg.png">

- digital data를 Modulation해서 analog signal로 전송
- analog signal을 Demodulation해서 다시 digital data로 수신
- digital data의 정보를 기반으로 analog signal의 특성(Amplitude, Frequency, Phase)을 변환

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfeLM2%2Fbtr9rhrcENu%2FThk9ESGFXzYhnf8ZYiDb4K%2Fimg.png">

## ASK

<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Fc953ae07-7f4d-41db-8bd6-6899a66e00b3%2Fimage.png">
  
   - Amplitude Shift Keying
   - Carrier signal의 amplitude에 변화를 줘서 신호 전송
   - frequency, phase는 변화 x

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FepWcny%2Fbtr9n5542BS%2FHE9OLxhbgK69EoOKgwuTaK%2Fimg.png">

  - 1일 때 진폭은 +, 0일 떄의 진폭은 0 또는 1일 때의 진폭보다 작은 진폭을 가짐
  - fc : carrier signal frequency
  - Bandwidth = (1 + d) * Signal rate, f max와 f min의 차이로 결정, (d = 0 ~ 1)
  - signal rate가 높다 == sine wave의 사이클 속도가 빠르다 -> frquency 증가
  - f min은 그대로인데 f max가 계속 증가하므로 필요한 BW의 크기도 증가

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoeZb6%2Fbtr9mkbOjEK%2FxW4k7WCm9WfKbco5ySfBNK%2Fimg.png">

  - 보통 full-duplex link를 사용하기 때문에 2개의 carrier frequency로 bandwidth를 둘로 나눔, 왼쪽 : tx, 오른쪽 : rx
  - 만약 fc1과 fc2가 너무 가까이 있으면 신호의 간섭이 발생, 더 큰 진폭이 나타날 수 있음

## FSK

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbUSIya%2Fbtr9rgFRfAI%2Fceb906C8PqiZpGurreu7rk%2Fimg.png">

  - Frequency Shift Keying
  - 0, 1을 보낼 때 서로 다른 frequency 사용
  - amplitude, phase는 변화 x
  - ask의 문제 해결, medium의 물리적 특성에 제한 받음
  - Bandwidth = (1 + d) * Signal rate + 2 * df
  - 위 그림에서 f1, f2를 중심으로 bandwidth가 (1 + d) * Signal rate
    - f min은 f1으로부터 (1 + d) * signal rate / 2만큼 차이
    - f max도 f2로부터 (1 + d) * signal rate / 2만큼 차이
    - f2 - f1 = 2 * df
   
## PSK

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F16kaH%2Fbtr9pccTYt7%2FQ3KRFkehlxbhjzNfXml8l0%2Fimg.png">

  - Phase Shift Keying
  - 0, 1이 서로 다른 phase, 일반적으로 180도 차이를 둔다고 함
  - frequency, amplitude 변화 x
  - 노이즈는 진폭에 영향을 주는데 psk는 진폭 변화가 없기 때문에 ask와 달리 노이즈에 덜 밀감
  - fsk만큼의 bandwidth 제한 x
  - Bandwidth = (1 + d) * Signal rate

## QPSK
   - 4 - PSK, signal level = 4, 1 signal이 2 bit를 받음
   - phase가 90도 차이로 변화
   - r = 2 -> Signal rate = Bit rate / 2
   - Bandwidth = (1 + d) * Signal rate / 2

<p align="left"><img width="250" height="350" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FczvqrA%2FbtsaESsiYDs%2FhPXuzkyWMRZFpVeNfTdwc0%2Fimg.png">
<p align="center"><img src="https://www.etti.unibw.de/labalive/experiment/qpsksignalgeneration/qpsk-symbols.png">

  - Constellation Diagram

<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Ff53bf3f3-1b61-4282-9352-3a9f97c9061e%2Fimage.png">
<p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2Fca7a7464-40b5-48f2-bbeb-af52a935b517%2Fimage.png">

  - length : Amplitude, angle : Phase
  - 하나의 신호를 좌표계로 표현 가능

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB0USB%2Fbtr9na7JemW%2FZ3Ap8aKg3wOiuKgKQgrRck%2Fimg.png">

  - ASK는 0일 때 진폭 0, 1일 때 진폭 nV로 반지름 차이 존재
  - BPSK는 180도 차이를 갖기 때문에 수평

# How cas I increase the "number of signal level"?

## QAM
- Quadrature Amplitude Modulation
- ASK + PSK, x : phase 변화, y : amplitude 변화
- ASK보다 노이즈에 덜 민감
- ASK, PSK와 같은 Bandwidth 필요

<p align="center"><img src="https://www.researchgate.net/profile/Diponkor-Bala/publication/348364945/figure/fig13/AS:978360553447425@1610270741941/Constellation-diagram-of-4-QAM-and-8-QAM.png">

- 왼쪽 : 4 - QAM (1 amplitude, 4 phase)
- 오른쪽 : 8 - QAM (2 amplitude, 4 phase)

## Bit / Baud Comparison
![image](https://github.com/user-attachments/assets/8c0229be-a729-40e7-85b5-fb6af90d1f13)

# 5.2 Analog-to-Analog Conversion