# How to convert data into signal?
- Encoding
    - digital/analog "data"를 digital signal로 변환하는 방법
    - 변환된 digital signal을 data로 다시 바꾸는 것은 Decoding이라고 함

- Modulation
    - encoding된 data를 "carrier signal"을 이용하여 analog signal로 변환하는 방법
    - source data에 따라 carrier signal의 특성을 변환

# 4.1 Digital-to-Digital Conversion
- Data element vs Signal element

    <p align="center"><img src="https://velog.velcdn.com/images%2F00springbom00%2Fpost%2F564e8cce-f909-4cd7-b5c2-6d10e4b9003f%2Fimage.png">

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