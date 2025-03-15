## Java 정리
### 기본 형태
```
package 폴더명;

public class 파일명{
        public static void main(String[] args){

        }
}
```
### 단축키 
```
main + ctrl + space  ->  main method 단축키
sysout + ctrl + space  ->  print 단축키
ctrl + f11  ->  실행 단축키
ctrl + /  ->  주석
ctrl + alt + ↑/↓  ->  복사
```
주석: //,   /* */
### Print
```
System.out.println();
Systme.out.printf();
%d, %(1.3)f, %s, %c

문자열 + 숫자 = 문자열
ex) System.out.println("result : " + 35)  -> type string
```
### 자료형
```
정수형  byte   char(unicode)   short   int   long
        1byte  2byte          2byte  4byte  8byte
실수형  float   double
        4byte   8byte
bool    boolean
        1byte
문자열 String

ex) float fvalue = 3.14f;  <- float 자료형에 담는 데이터 끝에 f 붙여야함
long lvalue =  30000000L   <-   L을 넣어줘야 long 타입 지정..?

char은 unsigned 자료형
byte 범위는 -128 ~ 127
```
### 캐스팅 연산자
```
(int),(char),(float),(long),(double)...

작은 자료형 = 큰 자료형 일 때 사용
ex) int i = 45;
    byte b = byte(i);

casting 할 때는 자료형 크기에 의한 데이터 손실 주의
```
