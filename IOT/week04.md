### 초음파 거리를 LCD에 출력

```
#include <Wire.h> // I2C 통신을 위한 기본 라이브러리 
#include <LiquidCrystal_I2C.h> // I2C LCD 라이브러리
#define trig 12
#define echo 13
LiquidCrystal_I2C lcd(0x27, 16, 2); // LCD 주소 ?

void setup() {
  pinMode(trig,OUTPUT);  
  pinMode(echo,INPUT);
  lcd.init();             // I2C LCD 초기화
  lcd.backlight() ;         // 백라이트 켬
  lcd.print("LCD init");
  delay(2000);              // 2초 대기
  lcd.clear();              // 화면 지우기
}

void loop() {
  long duration, distance;
  digitalWrite(trig,LOW);
  delayMicroseconds(2);
  digitalWrite(trig,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig,LOW);

  duration = pulseIn(echo,HIGH);
  distance = duration / 58.2;

  lcd.setCursor(0, 0);      // 첫 번째 행 첫 번째 열로 커서 설정
  lcd.print("distance=");
  lcd.print(distance);
  if(distance < 5){
    lcd.clear();
    lcd.print("too close");
  }
  delay(1500);
  lcd.clear();

  // for (int position = 0; position < 16; position++) {
  //   lcd.scrollDisplayLeft();  // 화면 왼쪽으로 스크롤
  //   delay(150);               // 150ms 대기
  // }
}
```
