## Wi-Fi
----------
### IEEE 표준에 따른 비교
| IEEE 표준 | 802.11b | 802.11a | 802.11g | 802.11n |
| ---------- | ------- | ----- |--------------| ----- |
| 주파수 대역 | 2400-2483.5MHz | 5150-5250MHz<br>5250-5350MHz<br>5725-5825MHz | 2400-2483.5MHz | 2.4GHz &<br> 5GHz |
| MAC | CSMA/CA | CSMA/CA | CSMA/CA | CSMA/CA |
| 전송 방식 | DSSS | OFDM | OFDM | OFDM/OFDMA<br>With MIMO |
| 변조 방식 | BPSK,QPSK,CCK | BPSK,QPSK,<br>16-64 QAM | CCK, QAM | Same |
| 도달 거리 | ~100m | ~50m | ~100m | ~100m, ~50m|

### Wi-Fi 구성
  * IEEE 802.11 Working Group에서 표준화 작업
  * AP (Access Point)와 station(STA)으로 구성
    * AP : 유무선 공유기, STA : 공유기에 연결될 수 있는 기기들(노트북, 스마트폰 등)

### Wi-Fi Service Set
  * BSS(Basic Service Set)\
    * AP가 없으면 ad host 모드
    * AP가 있으면 infrastructure 모드
  * ESS(Extended Service Set)
    * 두 개 이상의 BSS들이 모여서 구성

### MAC 방식
  * PCF(Point Coordination function)
    * Option
    * 중앙집중식 Polling 방식 사용
  * DCF(Distibuted coordination function)
    * CSMA/CA 사용, Station에서 사용

### MAC Dat Frame 
