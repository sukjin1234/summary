### C# 정리
```
C#은 객체지향 언어이다.
플랫폼이란 일반적으로 소프트웨어 응용 프로그램들을 실행하는데 사용되는 하드웨어와 소프트웨어의 집합이다.(ex 운영체제)
닷넷플랫폼(CLR)
```
## 자료형
```
byte 1byte unsigned 정수형 <-> ubyte
char 2byte(unicode) 문자형
short 2byte signed 정수형 <-> ushort
int 4byte 정수형    <-> uint
long 8byte 정수형   <-> ulong
float 4byte 실수형
double 8byte 실수형
string 문자열 자료형
bool 불 자료형
```
### namespace -> class -> main 
C#은 모든 자료형이 class로 만들어져있다.
## 기본구조
```
namespace FirstProgram   // 프로젝트 이름 
{
  internal class Program   // 파일 이름
  {
    static void Main(string[] args)
    {
      
    }
  }
}
```
### 수업정리
```
console.Write()
console.WriteLine()  -  출력

long.Parse()  -  타입을 long
short.Parse()  -  타입을 short
double.Parse()  -  타입을 double로 변경
int.Parse()  -  () 안에 타입을 int로 변경
.ToString()  -  . 앞에 타입을 string으로 변경
.GetType()   -  . 앞에 타입을 반환

string + int -> string   python과 다름
문자열 연결 연산자로 동작

string.Format("{0},{...}",변수명,...)  python과 같음
$"{변수명}"  -  문자열보간법

Environment.NewLine  == "\r\n"    - 줄바꿈과 같음(모든 운영체제에서 줄바꿈됨)

int,float,double,long ... 끼리는 캐스트 연산자 사용 가능 O
string만 불가 X

python처럼 string 인덱싱 가능
하지만 인덱싱하면 char 타입으로 바뀜
ex) text = "string";  -> type == string
    a = text[0]   -> type == char

정수 -> 실수 : OK
실수 -> 정수 : 처리필요
작은 타입 -> 큰 타입 : OK
큰 타입 -> 작은 타입: 처리필요 
```

ctrl 활용해서 ui 복사 가능
도구상자에 있는 공용컨트롤들은 int,float .. 같은 변수 | 안에 값을 넣어줘야 작동함

