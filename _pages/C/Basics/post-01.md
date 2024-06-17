---
title: "[C언어의 기본] #1"
date: "2024-06-17"
---

## C언어란?

C언어는 '프로그래밍 언어'이다.

*프로그래밍언어: 컴퓨터와 대화에서 사용되는 일종의 대화수단

A라는 사람이 한국어, 영어
B라는 사람이 영어, 일본어
C라는 사람이 일본어 

가능한다는 조건이 있다.

a -(영어) -> B -(일본어) -> C
이렇게 B라는 통역가를 통해서 A의 말을 C에게 전달하는 것이다.

프로그래밍에서는 컴파일러(Compiler)라는 통역가라는 것이 존재한다.

A라는 사람이 한국어, C언어
B컴파일러는 C언어, 기계어
C컴퓨터는 기계어

이렇게 위와 같이 A라는 사람의 C언어를 컴파일러를 통해 기계어로 해준다.

*프로그래밍언어는 사람과 컴파일러가 이해할 수 있는 약속된 형태의 언어로서 C언어도 프로그래밍언어이다. (java, C++, C#...)
*컴파일러는 프로그래밍언어로 작성된 프로그램을 컴퓨터가 이해할 수 있도록 기계어로 번역한다. 번역하는 일을 컴파일(Compile)이라 한다.
*기계어(Machine Language)? : 컴퓨터가 이해할 수 있는 0과 1로 구성된 언어 체계이다.

C언어의 장점
(1)절차지향적 특성 (순서대로 실행)
(2)이식성이 좋다 (CPU종류에 상관없고 운영체재 차이도 덜 민감)
(3)좋은 성능을 보인다. (메모리양이 상대적으로 적고, 속도 저하 요소가 최소화)

### 프로그램 완성과정

![](https://velog.velcdn.com/images/kikyo/post/8f730f97-e7d6-499e-8c80-c1bf45aabdbb/image.png)<br/>

프로그램 완성과정은 위와같다.

1.프로그램작성을 통해 소스파일(.c)파일을 생성한다.
2.컴파일을 통해서 오브젝트 파일(.obj)파일을 생성한다.
3.링크를 통해 실행파일(.exe)을 생성한다.
4.실행파일 생성 후 실행한다(cpu)

## 프로그램 기본구성

"C언어는 함수로 시작해서 함수로 끝난다"
C언어로 프로그램을 만드는 것은 '함수를 만들고, 함수의 실행순서를 결정하는 것'이다.

> 3x+4=y

예를 들면 x가 1이라는 가정하에 x에 1을 넣으면 7이 된다. 
여기서 x값을 입력, y값을 출력이라고 한다.
적절한 입력과 그에 따른 출력이 존재하는 것을 '함수'라 한다.

> int main (void)

이런 문구를 많이 볼 수 있는데 처음에는 이 뜻을 모르고 그냥 외우기만 했다. 
왜 int ? main ? void인가?
하지만 책을 통해 알 수 있었다.
int = 출력형태
main = 함수이름
void = 입력형태


'출력의 형태는 int, 입력의 형태가 void인, main함수이다'

>int main (void)
>{
> 함수의 몸체
>}

그리고 이러한 main함수의 기능을 담당하는 것이 함수의 몸체이다.

이것을 통해 나는
'void입력을 가지고 main 함수로 가져와 함수의 기능을 수행하여 int로 반환하라' 라고 알 수 있었다.


+ 함수 내에 존재하는 문장의 끝에는 세미클론 ;을 붙힌다. (문장의 끝을 표현)

### Hello World 알아보기

>printf("Hello World! \n");

어느 책이든 Hello World, Hello C World로 구성되는 것 같은건 기분 탓일까?
C언어는 " " 을 통하여 문자열을 표현한다. 위 문장은 "Hello World! \n"을 인자로 전달하면서
printf라는 이름의 함수를 호출하는 것이다.

+ printf라는 함수를 만든적이 없는데 어떻게 호출할 수 있는가? : 기본제공함수(표준함수)가 있기 때문이고 표준함수의 모임을 '표준라이브러리'라고 한다.

표준함수 호출을 위해서는 그에 맞는 헤더파일 선언이라는 것을 해야한다.
why? 도서관을 가져와 그에 필요한 책(헤더파일)을 부르듯이..

> #include <stdio.h>

stdio.h라는 확장자가 .h로 끝나는 헤더파일을 포함하라는 의미의 선언이다.
#(전처리기) include(포함하다) <stdio.h> (standard input/Output.Header - 표준입출력)

+ 헤더파일의 선언은 소스파일의 맨 앞부분,  main함수 정의 이전에 와야한다.

> return 0;

마지막에 위와같은 내용이 많이 붙는데 솔직히 몰랐다. ㅋㅋㅋ;;

위는 return문이라고 하는데 의미는 2가지이다.
(1)함수를 호출한 영역으로 값을 전달(반환)
(2)현재 실행중인 함수의 종료

return 0;는
OS에게 0을 전달하고 main 함수를 종료시키는 것이다.

return ;으로 한다면
반환할 값이 없으니 main 함수를 그냥 종료시키라는 것이다.

### 가지고 놀아보기

문제 1: 본인의 이름을 출력하는 프로그램을 작성해보자. 단 printf 함수를 한번만 호출해야한다.
1.홍길동
2.홍길 동
3.홍 길 동

```c
#include <stdio.h>
 int main (void)
 {
 	printf("홍길동\n홍길 동\n홍 길 동\n");
 	return 0;
 }
```

문제2: 본인의 이름, 주소, 전화번호를 출력하는 프로그램을 작성해보자 총 3번의 printf함수를 사용한다.

```c
#include <stdio.h>
int main (void)
{
	printf("이름: 홍길동\n");
    printf("주소: 서울특별시 어쩌구..\n");
    printf("전화번호: 010-1111-2222\n");
    return 0;
}
```

### 주석 이해하기

"주석은 선택이 아닌 필수이다!"

주석은  블록단위, 행단위가 있다.

```
블록단위 주석 /* */ (안의 내용은 전부 주석)
행단위 주석 //     (그 줄만 주석으로 처리) 
```

*프로젝트의 진행에 앞서 어떠한 형태로 어느 수준으로 주석을 달 것인지 결정하고 따른다고 한다.

```c
/*
제목 : Hello World 출력시키기
기능 : 문자열의 출력
파일이름 : HelloCommnet.c
수정날짜 : 2024.01.02
작성자 : 미누
*/

#include <stdio.h> //헤더파일의 선언

int main(void) //main함수 시작
{
	printf("Hello World! \n"); //문자열 출력
    return 0; //0을 반환시키기
}
```

주석은 간단하고 명료해야된다. 복잡하면 오히려 해가되니 조심하자!

+ 블록 단위의 주석은 중첩될 수 없다.

```
/*
 주석처리 된 문장
  /*단일 행 주석처리시키기 */
  주석처리 된 문장2
*/
```

1행에서 주석처리를 시작하고 2행과 3행이 주석처리되고 3행의 마지막 주석처리기 시키기 뒤에 주석끝으로 인식하고 4행과 5행은 주석으로 인식되지 않는다.


```
/*
 주석처리 된 문장
 // 단일행 주석처리
 주석처리 된 문장2
 */
```

위와 같이 바꾸게 되면 주석에는 이상이 없어지니 블록단위의 주석을 할떄는 주의하자!

### Printf 함수의 기본적인 이해

```c
#include <stdio.h>

int main(void)
{
	printf(Hello Everybody \n");
    Printf("%d\n", 1234);
    printf("%d %d\n", 10, 20);
    return 0;
}
```

실행결과를 보면

> Hello Everybody <br/>
> 1234 <br/>
> 10 20 <br/>

을 알 수 있듯이. 위의 프로그램 동작을 통해 C언어는 순차적으로 실행된다는 사실을 알 수 있다.
그리고 Printf를 통해서 함수를 이용하여 문자열, 정수데이터를 출력할 수 있음을 알 수 있다.

즉 'Printf 함수는 첫번째 인자로 전달된 문자열을 출력한다'

여기서 %d라는 것이 처음등장하게 되는데 이러한 문자를 가리켜 '서식문자(ConverSion Specifier)'이라고 한다.
출력의 형태를 지정하는 용도로 사용이 된다.

```c
Printf(인자1("%d\n"), 인자2(1234)); => printf("%d\n",1234)
```

>%d에 1234라는값이 들어가게 되어 출력문은 "1234\n"이 된다. <br/>

좀더 응용하면 printf("%d %d\n", 10, 20);을 보자.

```c
printf(인자1 ("%d %d\n"), 인자2(10),인자3(20)); => printf("%d %d\n", 10, 20);
```

> 첫번쨰 %d에는 인자2값 10, 두번쨰 %d에는 인자3값 20이 들어가게 되어 출력문은 "10 20\n"이 된다.

의외에도 서식문자가 많지만 진도를 나가면서 보여준다고 하셨으니 이정도만 기억하고자 한다.

또한 출력의 형태를 다양하게 조합가능 하다고 한다.

```c
#include <stdio.h>

int main(void)
{
	printf("My age: %d \n", 27);
    printf("%d is my point \n", 100);
    printf("Good \n moring \neverybody\n");
    return 0;
}
```

>My age: 27 <br/>
>100 is my Point <br/>
>Good <br/>
>moring <br/>
>everybody <br/>

출력이 되는 것으로 여러가지로 조합 할 수 있다.

다른 강의에서는 %d, %i (10진수 정수) , %x, %o  (16진수), %f, %lf(10진수 실수)
%c(문자) = ' ' , %s(문자열)= " ", %u(10진수의 정수 -양수) 가 있다고 해서 연습만 해보았다.

```c
#include <stdio.h>
int main(void)
{
	printf("10진수:%d는 16진수:%x, 8진수: %o 입니다. \n", 50,50,50);
	printf("10진수:%d는 16진수:%x, 8진수: %o 입니다. \n", -50, -50, -50);

	return 0;
}
```

> 10진수:50, 16진수:32 8진수: 62 입니다. <br/>
> 10진수 -50, 16진수fffffce, 8진수:377777777716입니다. <br/>

하단의 %x, %o를 적용한 곳은 음수출력이 되지 않기에 쓰레기 값으로 나온다는 사실을 알 수 있다.


### 가지고 놀아보기

문제1: 출력결과를 보이도록 작성해보자. 출력되는 숫자들(20, 123, 456)은 서식문자를 이용하여 출력하자.
 제 이름은 미누입니다.
 제 나이는 27살이고요.
 제가 사는 번지는 123-456입니다.

 ```c
#include <stdio.h>

int main(void)
{
	printf("제 이름은 미누입니다.\n");
     printf("제 나이는 %d이고요.\n",27);
     printf("제가 사는 번지는 %d-%d 입니다.",123,456);
     return 0;
}    
 ```

문제2: 출력결과를 보이도록 작성해보자. 출력되는 숫자들은 서식문자를 활용하자.

4x5=20 <br/>
7x9=63

```c
#include <stdio.h>

int main(void)
{
	printf("%dx%d=%d\n",4,5,20);
    printf("%dx%d=%d",7,9,63);
    return 0;
}    
```

혹시 곱셈을 이용한 것도 되는지 확인해보고 싶어졌다 해보자.

```c
#include <stdio.h>

int main(void)
{
	printf("%d*%d=\n",4,5);
    printf("%d*%d=\n",7,9);
    return 0;
}    
```

이렇게 하면 안되는 듯.. printf는 그냥 서식문자에 문자열을 박아주는 것 같다.
" " 사이의 계산식을 넣어도 구동이 안된다 

```c
#include <stdio.h>

int main(void)
{
	printf("%dx%d=%d\n", 4,5,4 * 5);
	return 0;
}
```

혹시 아예 서식문자에 대한 값을 넣어주고 마지막 값을 20이 아닌 4*5라는 계산식을 넣어주면 작동하는지 확인해봤다.
아주 잘된다. 하지만 나중에 수정이 어려울 거 같으니 변수를 이용하는게 훨 씬 이로울 것 같다.

## 변수와 연산자

```c
#include <stdio.h>

int main(void)
{
	3+4: //3과 4의 덧셈
	return 0;
}    
```

문제없이 출력되는 예제가 있다. C언어는 특정연산을 요구할때 사용하는 약속된 기호를 가리켜 '연산자(Operator)'라고 한다.
해당 프로그램을 실행하면 결과가 안나오는데 그는 출력값이 없기 떄문이다.

이를 변경해보자
'덧셈연산을 한 후 그 결과를 메모리 공간에 저장한다. 그리고 그 저장된 값을 출력한다.'

할 수 있게 된다면 다양한 형태로 출력할 수 있는데 이를 위해서는 덧셈결과를 저장하기 위해 변수(variable)를 이용해야한다.

```c
int main(void)
{
	int num; //num변수 선언
	....
}
```

위를 참고하면 int와 num이 등장한다.
int 정수의 저장이 가능한 메모리 공간을 할당한다.
num 메모리 공간의 이름을 num이라 지정한다.

+ 정수는 -1, 0, 1...
+ 실수는 1.2, 1.3, 3.1 ...

이렇게 서식문자와 변수를 사용하면 변경할 수 있게 된다.

```c
#include <stdio.h>
int main(void)
{
	int num;  // 변수 num 선언
    num=20;  //변수 num에 값 20을 저장
    print("%d", num); // 변수 num 값을 참조하여 출력
}
```

선언된 변수를 처음 값을 저장하는 것을 가리켜 '초기화'라고 한다. 
초기화 이후 저장된 값을 변경할 떄에는 '대입'또는 '대입연산'을 진행한다고 한다.
변수를 통해 '선언과 동시에 초기화' 하는것이 가능하다.

```c
int num=12;
```

해당연산을 실행하게 되면, 변수 num이 메모리 공간을 할당 받자마자 12로 초기화 된다.
그리고 다음 둘 이상의 변수를 동시에 선언도 가능하고 동시에 선언 및 초기화도 가능하다.

```c
int num1, num2; //변수 선언
int num3=30, num4=40; // 선언 및 초기화
```

좀 더 구체적인 예를 보자

```c
#include <stdio.h>

int main(void)
{
	int num1, num2; //변수 num1, num2의 선언
    int num3=30, num4=40; //변수 num3, num4의 선언 및 초기화
    
    printf("num1: %d, num2: %d \n",num1,num2);
    num1=10; // num1 초기화
    num2=20; // num2 초기화
    
    printf("num1: %d, num2: %d \n",num1,num2);
    printf("num3: %d, num4: %d \n",num3,num4);
    return 0;
}    
```

>구동이 되지 않은데 아마도 쓰레기값이 발생해서 그런 것 같다. <br/>
>num1: 쓰레기값 , num2:쓰레기값 <br/>
>num1: 10 , num2: 20 <br/>
>num3: 30 , num4: 40 <br/>

+ 변수 선언시 주의 할 사항
  "중괄호 내에 변수를 선언할 경우, 변수의 선언문은 중괄호의 앞부분에 위치해야 한다."

```c
int main(void)
{
 int num1; //앞부분에 위차한 선언문
 int mun2;
 num1=0; //변수 선언 이후에 등장한 초기화 문장
 num2=0; //변수 선언 이후에 등장한 초기화 문장
 ...
} 
```

1999년도 발표된 C언어표준에서는 변수의 선언문 위치에 아무런 제한을 두지 않는다고 한다.
하지만 아직 상당수의 컴파일러가 변수 선언문 앞 부분을 요구하니 주의하자!

변수 선언시 주의해야 되는 점이 있다.

1. 변수의 이름은 알파벳, 숫자, 언더바(_)로 구성된다.
2. 변수의 이름은 대소문자를 구별한다. num!=Num
3. 변수의 이름은 숫자로 시작할 수 없고,키워드도 변수의 이름으로 사용할 수 없다.
4. 이름 사이에 공백이 삽입될 수 없다.

```
int 7sadkmsakd <불가능
int korea# <특수문자 불가능
int Poker game <공백 발생
```

그리고 "변수의 이름을 정할때는 의미 있는 이름을 지어야한다." <이게 제일 어렵다고 합니다..

### 변수의 자료형

변수는 크게 2가지로 나뉜다.
1.정수형 변수  = int, char, short, long ..
2.실수형 변수  = float, double ..

2가지로 나뉘는 이유는 정수냐, 실수냐에 따라서 값이 메모리 공간에 저장 및 참조되는 방식이 다르기 때문이다.
(정수와 실수의 저장방식이 다르다)


```c
int num1=24; // num1을 가리켜 int형 변수
double num2=3.14; //num2를 가리켜 doulbe형 변수
```

### 덧셈 프로그램의 완성

```c
#include <stdio.h>

int main(void)
{
	int num=3;
    int num=4;
    int result=num1+num2;
    
    printf("덧셈결과: %d \n", result);
    printf("%d+%d=%d \n", num1, num2, result);
    printf("%d와 %d의 합은 %d입니다.\n", num1, num2, result);
    return 0;
}    
```

>덧셈결과: 7 <br/>
>3+4 = 7 <br/>
>3와 4의 합은 7입니다. <br/>

+ 단항 연산자와 이항연산자

단항연산자는 피연산자의 개수가 1개 - ex) ++num 
이항연사자는 피연사자의 개수가 2개 - ex) 3+4

### 다양한 연산자 소개

```
| 연산자 |            기능                          | 결합방향 |
|  =    | 오른쪽 값을 왼쪽에 대입함                   | <-     | 
|  +    | 두 피연산자의 값을 더한다                   | ->     |
|  -    | 왼쪽 값에서 오른쪽 값 뺀다                  | ->     |
|  *    | 두 피연산자의 값을 곱한다                   | ->     |
|  /    | 왼쪽 값에서 오른쪽 값을 나눈다              | ->      |
|   %   | 왼쪽 값에서 오른쪽 값을 나눈 나머지 값을 반환 | ->      |
```

연산자의 사용 예를 한번 보도록 하자.

```c
#include <stdio.h>

int main(void)
{
	int num1=9, num2=2;
    printf("%d+%d=%d \n", num1, num2, num1+num2);
    printf("%d-%d=%d \n", num1, num2, num1-num2);
    printf("%dx%d=%d \n", num1, num2, num1*num2);
    printf("%d/%d=%d의 몫 \n", num1, num2, num1/num2);
    printf("%d/%d=%d의 나머지 \n", num1, num2, num1%num2);
    return 0;
}    
```

>9+2=11 <br/>
>9-2=7 <br/>
>9x2=18 <br/>
>9/2의 몫 =4 <br/>
>9/2의 나머지 = 1<br/>

위를 통해 "함수 호출문이 인자전달 위치에 연산식이 올수 있다."
아까 연습했던게 여기에 나온 것 같다 굿굿

그리고 num1+num2부분에서 우선연산이 실행된다.

### 복합대입연산자

*=,/=,%=,+=,-=,<<=,>>=,&=,^=,/=

```
a= a+b <=> a +=b
a= a-b <=> a -=b
a= a*b <=> a *=b
a= a/b <=> a /=b
a= a%b <=> a %=b
```

대충 겹치는 부분을 사라지게 해서 코드를 더  짧게 하는 것 일지도?

```c
#include <stdio.h>

int main(void)
{
	int num1=2, num2=4, num3=6;
    num1 +=3;
    num2 *=4;
    num3 %=5;
    printf("Result: %d, %d, %d \n", num1, num2, num3);
    return 0;
}    
```

>Result : 5, 16, 1

num1 +=3 은 num1=num1+3; = 5 <br/>
num2 *=4 는 num2=num2*4 = 16 <br/>
num3 %=5 는 num3=num3%5 = 1 <br/>

+ 주의할점
  주의 할점으로는 부호연산과 헷갈리지 않도록 조심해야한다.

```c
#include <stdio.h>

int main(void)
{
	int num1  = +2;
    int num2  = -4;
    
    num1 = -num1;
    printf("num1: %d\n",num1);
    num2 = -num2;
    printf("num2: %d\n",num2);
    return 0;
}   
```

>num1 = -2  <br/>
>num2 = 4 <br/>

위처럼 헷갈릴 수 있다고 한다. <br/>

num1=-num2; //부호 연산자 <br/>
num1-=num2; // 복합대입연산자 

그래서 공백을 두는 것이 혼란을 최소화 할 수 있다. <br/>

num1 = -num2; <br/>
num1 -= num2; 

### 증가, 감소 연산자

![](https://velog.velcdn.com/images/kikyo/post/0518d8bc-9c47-4db3-a69a-6ed34527d4aa/image.png)<br/>
표를 그리기 어렵기에 사진으로 대체한다..;;
위처럼 앞이냐 뒤냐에 따라 나뉜다.

```c
#include <stdio.h>

int main(void)
{
	int num1=12;
    int num2-12;
    
    printf("num1= %d \n", num1);
    printf("num1++= %d \n", num1++);
    printf("num1= %d \n", num1);
    
    printf("num2= %d \n", num1);
    printf("num2++= %d \n", ++num1);
    printf("num2= %d \n", num1);
}    
```

>num1: 12 <br/>
>num1++: 12 <br/>
>num1: 13 <br/>
>num2: 12 <br/>
>++num2: 13 <br/>
>num2:13 <br/>

선연산 후 증가인지 선증가 후연산에 따라 다르다.

```c
#include <stdio.h>

int main(void)
{
	int num1=10;
    int num2=(num1--)+2;
    
    printf("num1: %d \n", num1);
    printf("num2: %d \n", num2);
    return 0;
}
```


>num1: 9 <br/>
>num2: 12 <br/>

이를 보면 int num2 =(num1--)을 통해 num1은 num2의 초기화 이후 9로 변하게 되어 printf를 통해 9로 보인다.
int num2는 10+2를 시킨 후 num1이 떨어진 것이기 때문에 num2= 12가 출력된다.

but) ++num이 아닌 ++3은 실행되지 않는다. 변수의 지정한 값을 변형시키는 것이기 때문이다.

이것을 통해 '소괄호의 영향을 받지 않고, 다음 문장으로 넘어가야만 비로소 값의 증가 및 감소가 이뤄진다'

### 관계연산자

![](https://velog.velcdn.com/images/kikyo/post/36adfba0-82b4-410b-9581-6d3e45ccda86/image.png)<br/>

조건을 만족하면 1을 , 만족하지 않으면 0을 출력한다. (true, false)

```c
#include <stdio.h>

int main(void)
{
	int num1=10;
    int num2=12;
    int result1, result2, result3;
    
    result1=(num1==num2);
    result2=(num<=num2);
    result3=(num>=num3);
    
    printf("result1: %d \n", result1);
    printf("result2: %d \n", result2);
	printf("result3: %d \n", result3);
    return 0;
}
```

>result1: 0 <br/>
>result2: 1 <br/>
>result3: 0 <br/>

첫번째는 10과 12가 같지 않으니 0 <br/>
두번쨰는 12가 10보다 크니 1 <br/>
세번째가 10이 12보다 작으니 0 <br/>

즉 result1은 num1 ==num2의 ture(1)값을 반환한 것이다.

### 논리연산자

![](https://velog.velcdn.com/images/kikyo/post/3ac782ce-0c46-4992-80aa-2ac039c959d3/image.png)

논리연산은 디지털 논리회로의 AND, OR, NOT 과 같으니  <br/>
&&, ||, !를 들어다본다.

```c
#include <stdio.h>

int main(void)
{
	int num1=10;
    int num2=12;
    int result1, result2, result3;
    
    result1=(num1==10 && num2==12);
    result2=(num<12 || num2>12);
    result3=(!num1);
    
    printf("result1: %d \n", result1);
    printf("result2: %d \n", result2);
	printf("result3: %d \n", result3);
    return 0;
}
```

>result1 = 1 <br/>
>result2 = 1 <br/>
>result3 = 0 <br/>

이를 보면
result1은 num1==10 AND num2=12이기에 num1==10은 true(1), num2==12는 true(1)이기에 true true로 1이다. <br/>
result2는 num1<12 OR num2>12 이기에 num1<12은 true(1), num2>12은 false(0)이기에 ture false로 1이다. <br/>
result3은 1이상의 값은 True로 인식되기에 true의 not인 false(0)이 출력된다. <br/>

즉 "C언어는 0이 아닌 값은 참(true)으로 간주한다'라는 것을 알 수 있다.

### 콤마 연산자

둘 이상의 변수를 동시 선언하거나, 둘 이상의  문장을 한행에 삽입하는 경우이며 구분을 목적으로 주로 사용한다.

```
#include <stdio.h>

int main(void)
{
	int num1=1, num2=2;
    printf("Hello "),printf("World! \n");
    num1++, num2++
    printf("%d",num1), printf("%d", num2), printf("\n");
    return 0;
}    
```

>Hello World!
>2 3

으로 문장을 여러개 삽입하여 출력할 수 있음을 알게됐다.

### 연산자의 우선순위와 결합방향

![](https://velog.velcdn.com/images/kikyo/post/2f205f0e-c6ad-41a4-ab97-71873799e55f/image.png)<br/>

우리가 +,-,*,/ 처럼 사칙연산의 우선순위가 있는것 처럼 연산자도 우선순위가 있다.
+결합방향도 있는데 이건 외우기보다는 천천히 익혀가는게 좋을 것 같다.;;

### Scanf 함수

scanf 함수를 활용하면 키보드로 입력받은 형태의 데이터를 받을 수 있다.

```c
int main(void)
{
	int num;
    scanf("%d", &num);
    ...
}    
```

이것을 통해 %d = 10진수 정수 형태로 입력받아서 num변수에 저장하라는 것이다.

+ 변수 num 앞에 연산자 &는?
  해당 이유는 주소값 반환이지만 일단 지금은 scanf함수의 호출을 위해서는 저장할 변수 이름 앞에 &를 붙힌다고만 알자.

```c
#include <stdio.h>

int main(void)
{
	int result;
    int num1, num2;
    
    printf("정수 One: ");
    scanf("%d", &num1);
    printf("정수 Two: ");
    scanf("%d", &num2);
    
    result=num1+num2;
    printf("%d + %d = %d \n", num1, num2, result);
    return 0;
}    
```

뭐지 출력이 안된다..; <br/>
scnaf의 반환값이 무시된다고 한다.

구글링 해보니까  <br/>
앞에 # pragma warning(disable:4996)를 붙혀주면 된다고 한다.

>정수 One: 1 <br/>
>정수 Two: 2 <br/>
>를 입력하니 <br/>
>1+2=3이 나왔다. <br/>

### 입력의 형태를 다양하게 지정가능

```c
int main(void)
{
	int num1, num2, num3;
    scanf("%d %d %d", &num1, &num2, &num3);
    ...   
}   
```

3개의 10진수 정수를 입력가능하다.

```c
#include <stdio.h>

int main(void)
{
	int result;
    int num1, num2, num3;
    
    printf("세 개의 정수를 입력: ");
    scanf("%d %d %d", &num1, &num2, &num3);
    
    result=num1+num2+num3;
    printf("%d + %d + %d = %d \n", num1, num2, num3, result);
    return 0;
}    
```

오류가 나서 다시 위의 값을 붙혀준 후 실행한다.

>세 개의 정수를 입력 3 4 5  <br/>
>3 + 4 + 5 = 12 <br/>

scnaf함수는 공백을 기준으로 데이터를 구분하는 것을 알 수 있다.

### 가지고 놀아보기

문제1: 프로그램 사용자로부터 두개의 정수를 입력받아서 두 수의 뺄셈과 곱셈의 결과를 출력하는 프로그램 작성하기

```c
#include <stdio.h>

int main(void)
{
	int num1,num2;
    printf("두 개의 정수를 입력하세요: ");
    scanf("%d %d",&num1,&num2);
    printf("%d - %d = %d \n", num1, num2, num1-num2);
    printf("%d x %d = %d \n", num1, num2, num1*num2);
    return 0;
}    
```

>두 개의 정수를 입력하세요 : 3 4 <br/>
>3 - 4 = -1 <br/>
>3 x 4 = 12 <br/>

문제2: 세개의 정수를 순서대로 입력받은 후 다음 연산의 결과를 출력하는 프로그램을 작성하라. <br/>

(num1xnum2+num3)

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1,num2,num3;
    printf("세 개의 정수를 입력하세요: ");
    scanf("%d %d %d", &num1, &num2, &num3);
    printf("%dx%d+%d=%d\n", num1, num2, num3, num1*num2+num3);
    return 0;
}    
```

>세 개의 정수를 입력하세요: 1 2 3 <br/>
>1x2+3=5

문제3: 하나의 정수를 입력받아서 그 수의 제곱의 결과를 출력하는 프로그램을 작성해보자.

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1;
    printf("정수 값을 입력하세요: ");
    scanf("%d", &num1);
    printf("%d 의 제곱값은 %d 입니다\n", num1, num1*num1);
    return 0;
}    
```

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1;
    printf("정수 값을 입력하세요: ");
    scanf("%d", &num1);
    printf("정수 값의 제곱은 %d 입니다\n", num1*num1);
    return 0;
} 
```

>정수 값을 입력하세요: 3 <br/>
>정수 값의 제곱은 9입니다. <br/>
>3의 제곱값은 9입니다. <br/>

문제4: 입력 받은 두 정수를 나누었을 때 얻게 되는 몫과 나머지를 출력하는 프로그램을 작성하세요.

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1, num2;
    printf("두 개의 정수를 입력하세요: ");
    scanf("%d %d", &num1, &num2);
    printf("몫의 값은 : %d , 나머지의 값은 %d 입니다", num1/num2, num1%num2);
    return 0;
}
```

>두 개의 정수를 입력하세요: 3 6  <br/>
>몫의 값은 0 , 나머지의 값은 3입니다. <br/>

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1, num2;
    printf("두 개의 정수를 입력하세요: ");
    scanf("%d %d", &num1, &num2);
    printf("%d/%d의 몫의 값은 : %d , %d % %d 나머지의 값은 %d 입니다", num1,num2,num1/num2,num1,num2, num1%num2);
    return 0;
}
```

>두 개의 정수를 입력하세요: 3 6 <br/>
>3/6 몫의 값은 0, 3 %d 나머지의 값은 6입니다. <br/>

흠.. 뭔가 이상하다. % %d에서 인식을 못하는 것 같다.
어떻게 풀어야할까? 잘 모르겠다... 

%는 서식문자 지정기호이므로 %를 표현하려면 %%라고 해야된다고 한다.
그러면 이렇게 정리할 수 있겠다.

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
    int num1, num2;
    printf("두 개의 정수를 입력하세요: ");
    scanf("%d %d", &num1, &num2);
    printf("%d/%d의 몫의 값은 : %d , %d %% %d 나머지의 값은 %d 입니다", num1, num2, num1 / num2, num1, num2, num1 % num2);
    return 0;
}
```

문제5: 입력받은 세 개의 정수를 대상으로 다음의 연산 결과를 출력하는 프로그램을 작성해보자. <br/>

(num1-num2)x(num2+num3)x(num3%num1)

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1, num2, num3;
    int result;
    printf("세 개의 정수를 입력하세요: ");
    scanf("%d %d %d", &num1, &num2, &num3);
    result=(num1-num2)x(num2+num3)x(num3%num1);
    printf("정답: %d \n", result);
    return 0;
}    
```

```c
#include <stdio.h>
# pragma warning(disable:4996)

int main(void)
{
	int num1, num2, num3;
    printf("세 개의 정수를 입력하세요: ");
    scanf("%d %d %d", &num1, &num2, &num3);
    printf("정답: %d \n", (num1-num2)*(num2+num3)*(num3%num1);
    return 0;
}    
```

>세 개의 정수를 입력하세요: 1 2 3 <br/>
>정답: 0

아무래도 result 를 사용하는게 나중에 더 유지보수 하기 편할 것 같기에 묶어주는 것도 좋은 것 같다.

### C언어의 표준 키워드

auto,
_bool,
break,
case,
char,
_complex,
const,
continue,
default,
do,
double,
else,
enum,
extern,
float,
for,
goto,
if,
_Imaginary,
return,
restrict,
short,
signed,
sizeof,
static,
struct,
switch,
typedef,
union,
unsigned,
void,
volatile,
while,

등이 있다고 하며
프로그래머가 다른용도로 사용할 수 없도록 제한되어 있다고 한다.!