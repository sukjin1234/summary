## Wi-Fi
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
![Image](https://github.com/user-attachments/assets/aabe3bd2-b8b1-4926-8671-136869816b7f)
* FC : 패킷에 보내는 설정 정보가 들어있음
* Frame body : 보낼 내용
* MAC 주소 4개가 사용됨

### 주소 체계
![Image](https://github.com/user-attachments/assets/849b60b7-eb26-43d1-976e-500c9fbfe0d4)

| To DS | From DS | Address1 | Adress2 | Adress3 | Adress4 |
|-------|---------|----------|---------|---------|---------|
| 0 | 0 | Destination | Source | BSS ID | N/A |
| 0 | 1 | Destination | Sending AP | Source | N/A |
| 1 | 0 | Receiving AP | Source | Destination | N/A |
| 1 | 1 | Receiving AP | Sending AP | Destination | Source |

---

## MAC 
### CSMA-CA
 * Carrier sense Multiple Access with Collision Avoidance
 * CS (Carrier Sense) : 네트워크가 현재 사용중인지 알아냄
 * MA (Multiple Access) : 네트워크가 비어있으면 누구든 사용 가능
 * CA (Collision Avoidance) : 충돌 회피

### 충돌 (Collision)
 * 두 개 이상의 노드가 같은 시간대에 같은 노드에게 패킷을 전송
 * 수신 측은 데이터를 제대로 읽을 수 없게 됨
 * 충돌을 방지하고자, 채널이 사용되지 않는 것 같아도 랜덤한 시간 동안 백오프함(기다림)
 * RTS, CTS 를 사용하면, 충돌이 발생할 확률이 줄어듦

### Hidden Terminal Problem (숨겨진 노드 문제)
![Image](https://github.com/user-attachments/assets/88ff80f8-edef-4cba-88e4-689ce5746465)

 * 중간 터미널(A)은 양쪽 터미널(B,C)와 통신이 가능
 * 양쪽 터미널(B,C)는 서로 통신을 감지하지 못함
    * 신호 전송 범위가 달라서 서로의 존재를 알 수가 없음
    * 즉, Carrier Sening이 힘듦 -> RTS, CTS를 사용하는 이유

### 일반적인 CSMA-CA 동작 방식 (무선 랜 등에서 사용)
 * 경합 방식 : 채널을 사용하고자 하는 기기들끼리 경쟁
   1. 기기 A는 다른 기기가 데이터를 송신중인지 감지
   2. 만약 송신중이라면 대기한다(백오프)
   3. 송신 시작까지의 시간은 랜덤 한 시간이 할당된다.
   4. 기다린 후, 다시 반송파 감지를 해서 다른 반송파가 있는지 확인
   5. 데이터 전송을 시작.
    * 단계 1: 송신 단 -> 수신 단 : RTS(Request To Send)
    * 단계 2: 수신 단 -> 송신 단 : CTS(Clear To Send)
    * 단계 3: 송신 단 -> 수신 단 : Data 전송
    * 단계 4: 수신 단 -> 송신 단 : ACK(ACKnowledgement)
```
  송신 측에서 RTS 전송 후, 수신 측에서 CTS 전송
  송신 측에서 CTS를 전송 받지 못하면, 일정 시간 대기 후, RTS를 다시 전송
```

