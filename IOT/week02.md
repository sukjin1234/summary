```
arduino는 아날로그 신호를 받을 수만 있음
데이터를 받는 핀은 INPUT
데이터를 보내는 핀은 OUTPUT
```
### 초음파 거리에 따른 LED 제어
```
#define TRIG 13
#define ECHO 12

void setup()
{
  Serial.begin(9600); // Serial 통신을 9600 속도로 하겠다
    				// arduino에 연결하는 usb포트가 전원공급, 데이터전송
  pinMode(7,OUTPUT);
  pinMode(8,OUTPUT);
  pinMode(TRIG,OUTPUT);
  pinMode(ECHO,INPUT);

}

void loop()
{
  long duration, distance;
  
  digitalWrite(TRIG,LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG,HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG,LOW);
  
  duration = pulseIn(ECHO,HIGH);
  distance = duration / 58.2;
  Serial.print(distance);
  Serial.println(" Cm");

  if(distance >= 100){
    digitalWrite(7,HIGH);
    digitalWrite(8,LOW);
  } else{
    digitalWrite(8,HIGH);
    digitalWrite(7,LOW);
  }
  
  delay(1000);
}
```
