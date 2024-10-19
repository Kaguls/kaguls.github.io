---
title: "[C언어의 기본] 함수와 전역지역변수"
date: "2024-07-23"
thumbnail: "/assets/img/thumbnail/C.png"

---

# C언어의 함수

C언어의 핵심은 포인터가 아닌 함수라고 한다.

지금까지 예제 중에서 포인터는 없어도 함수는 무조건 있다.

함수를 잘 구성하고 활용하는 프로그래머가 실력있는 프로그래머다.

거기에는 어느정도의 시간과 경험이 필요하다.



## 함수의 정의와 선언

기본적으로 출력형태는

`int main (void)`처럼 반환형태(출력) / 함수이름 / 입력형태 다.

다시 한번 상기시키자.



1. 함수를 만드는 이유

일을 하는 것에 있어서 문제를 작게 나누어서 하나씩 해결하는 것이 중요하듯, 프로그램의 구현도 같다.

구현을 하기 위해서는 구현에 필요한 기능을 분석하고 결과를 바탕으로 작은 크기의 함수를 디자인 해야한다.



"Divide and Conquer" - 나누어서 정복하라



함수는 크다고 해서 좋은것이 아닌 하나의 함수는 하나의 기능을 하는 소소익선이다.

[하나의 기능은 주관적인 기준이다]



2. 함수의 입력과 출력: Printf함수도 반환을 한다.

우리가 이전에 배우듯 전달인자가 없거나 반환 값이 없는 경우가 있다.

이것을 통해서 우리는 "입력 또는 출력이 없는 함수도 존재한다(만들 수 있다)"



```c
int main(void)
{
	int num1, num2; //쓰레기값
	num1 = printf("12345\n"); //6 12345+\n1
	num2 = printf("I love my home\n"); //I love my home 11 V=3 \n=1 =15
	printf("%d %d \n", num1, num2);
	return 0;
}
```

이 예제를 실행해보면 Printf 함수에서 문자열의 길이를 반환한다.

num1에는 `12345+ \n`으로 총 6개의 문자열

num2에는 `I()love()my()home\n`으로 영어 11개 + \n 1개 + 띄어쓰기 4개로 총 16개의 문자열



#### 전달인자의 유무와 반환 값 유무에 따라 함수는 나뉜다.

유형 1 : 전달인자가 있고, 반환 값이 있다. 

유형 2 : 전달인자가 있고, 반환 값이 없다.

유형 3 : 전달인자가 없고, 반환 값이 있다.

유형 4 : 전달인자가 없고, 반환 값이 없다.



1. **전달인자와 반환값이 모두 있는 경우**

조건1)전달인자는 <u>int형 정수 둘</u>이며 이 둘을 이용한 <u>덧셈</u>진행

조건2)덧셈결과는 <u>반환</u>이 되며 따라서 <u>반환형도 int형</u>으로 선언한다.

조건3)<u>함수이름은 Add</u>라한다.

```c
int add(int num1, int num2)
{
	int result = num1 + num2; 
	return result; //result에 저장된 값을 Add함수를 호출 영역 전달
}
```



```c
int add(int num1, int num2)
{
	return num1 + num2;
}

int main(void)
{
	int result;
	result = add(3, 4); //변환 값을 대체됨  이때 int add를 실행함.
	printf("덧셈결과1: %d\n", result);
	result = add(5, 8); // 변화값 대체, 이때 int add다시 실행
	printf("덧셈결과2: %d\n", result);
	return 0;
}
```

여기서 return num1+num2; 처럼 결과를 바로 반환할 수 있으며

result=add(3,4)로 함수 호출문이 반환 값으로 대체될 수 있다.



즉 result = add(3,4)에서 위 int  add가 한번 써지고

result = add(5,8)에서 int add가 한번 써지는 것이다.



2. **전달인자나 반환 값이 존재하지 않는 경우**

printf는 서식을 지정해야되기 때문에 빈번히 호출하기 번거롭기 때문에

서식지정을 매번 하지 않아도 되도록 함수를 정의한다.



(인자전달 O , 반환 X)

```c
void showAddResult(int num) //인자전달 O 반환 X
{
	printf("덧셈결과 출력: %d \n,num2);
}
```

void로 반환(출력)은 X int num으로 입력 인자전달은 O이다.

몸통을 보면 return이 없다. 반환 값이 없기 때문에



(인자전달 X, 반환 O)

```c
int num ReadNum(void)
{
	int num;
	scanf("%d", &num);
	return num;
}
```

호출하기 편리하도록  정의하는 것



(인자전달 X, 반환 X)

```c
void HowtouseThisProg(void)
{
	printf("두 개의 정수 입력 덧셈결과\n");
	printf("두 개의 정수 입력하세요\n");
}
```

단순하게 메시지를 전달하기 때문에 인자의 전달과 값의 반환이 필요없다.



```c
int add (int num1, int num2) // O O
{
	return num1 + num2;
}

void showAddResult(int num) // X O
{
	printf("덧셈결과 출력: %d \n", num);
}

int ReadNum(void) // O X
{
	int num;
	scanf("%d", &num);
	return num;
}

void HowToUseThisProg(void) // X X
{
	printf("두 개 정수 입력시 덧셈출력\n");
	printf("두 개 정수 입력하세요. \n");
}

int main(void) 
{
	int result, num1, num2;
	HowToUseThisProg(); //printf출력
	num1 = ReadNum(); //num1에 ReadNum 값 대입 12 
	num2 = ReadNum(); //num2에 ReadNum 값 대입  24
	result = add(num1, num2); //결과 ADD 함수이용
	showAddResult(result); //값 출력 printf
	return 0;
}
```

위에서 사용한 모든 경우의 수로 코드를 만든 것이다.

이를 통해서 좀 더 자세히 알 수 있다!



#### return이 지니는 두가지 의미 중 한 가지 살리기

리턴문은 두 가지가 의미가 있다.

- 함수를 빠져나간다
- 값을 반환한다.

간혹 반환형이 void로 선언된 함수에 못쓰는건가? 할 수 있지만 쓸 수 있다.



```c
void NoReturnType(int num)
{
	if (num < 0)
		return; //반환하지 않는 리턴문 - 값 출력X
	....
}
```

`return ;`값을 반환하지 말고 빠져나가라. 

함수를 빠져나간다는 의미를 지정했다.



## 함수의 정의와 그에 따른 원형의 선언

함수의 위치를 결정할 때에도 주의를 기울여야 한다.

```c
int Increment(int n)
{
	n++;
	return n;
}

int main(void)
{
	int num = 2;
	num = Increment(num);
	return 0;
}
//가능
```

```c
int main(void)
{
	int num = 2;
	num = Increment(num);
	return 0;
}

int Incremnet(int n)
{
	n++;
	return n;
}
//불가능
```

가능은 위에서 함수를 알려주었기 때문에 메인이 읽을 수 있지만

불가능은 위에서 함수가 없기 때문에 인지하지 못한다.



```c
int Increment(int n);; //생략가능 (int)
int main(void)
{
	int num = 2;
	num = Increment(num);
	return 0;
}

int Increment(int n)
{
	n++;
	return n;
}
```

이렇게 먼저 main함수에게 밑에 int Increment라는 함수가 있다는 것을 귀띰해준다.

그러면 아 뒤에 있겠구나 ok하고 읽을 수 있게 된다.

`int Incremnet(int)`로 매개변수의 이름을 생략할 수도 있다. 



#### 다양한 종류의 함수 정의하기

"하나의 함수 내에 둘 이상의 리턴문이 존재하는 경우"



```c
int numCompare(int num1, int num2);

int main(void)
{
	printf("3과 4중 큰 수 %d\n", numCompare(3, 4));
	printf("7과 2중 큰 수 %d\n", numCompare(7, 2));
}

int numCompare(int num1, int num2)
{
	if (num1 > num2)
		return num1;
	else
		return num2;
}
```

완전하지 못하지만 `int numCompare`에 리턴문이 2개가 들어가있다.

이 예제를 통해 retrun문이 실행되면 값을 반환하면서 빠져나간다. 를 알 수 있었다.



```c
int AbsoCompar(int num1, int num2); //절대값 큰것
int GetAbsoValue(int num); //전달인자 절대값

int main(void)
{
	int num1, num2;
	printf("두 개의 정수 : ");
	scanf("%d %d", &num1, &num2);
	printf("%d와 %d중 절댓값이 큰 정수 : %d \n", num1, num2, AbsoCompar(num1, num2)); //비교호출
	return 0;
}

int AbsoCompar(int num1, int num2) //큰 값 비교 함수
{
	if (GetAbsoValue(num1) > GetAbsoValue(num2)) //절대값 호출
		return num1;
	else
		return num2;
}

int GetAbsoValue(int num) //절대값 함수
{
	if (num < 0)
		return num * (-1);
	else
		return num;
}
```

절대값이 큰 수를 알려주는 프로그램이다.

음수를 알려주면 `int GetAbsoValue`에서 음수면 음값을 곱해주어 양수로 교환해준다.

`int AbsoCompar`에서는 절대값을 비교하여 옳은 값을 리턴(반환)해준다.



#### 문제 [다양한 함수 정의하기]

**문제1:** 

<u>세 개의 정수를 인자</u>로 전달받아 그 중 가장 <u>큰 수를 반환하는 함수</u>와 <u>가장 작은 수를 반환하는 함수</u>를 정의하자.

이 함수들을 호출하는 <u>main함수도 작성</u>해보자.

```c
int upper(int num1, int num2, int num3); //큰 수
int lower(int num1, int num2, int num3); //작은 수
int checker(int check); //체크 수

int main(void)
{
	int num1, num2, num3; //
	int check;
	printf("비교할 3개의 정수 입력: \n");
	scanf("%d %d %d", &num1, &num2, &num3);
	printf("1. 큰 수 반환 2.작은 수 반환 입력\n");
	scanf("%d", &check);

    //조건문으로 큰수를 할지 작은 수를 할지 지정
	if (check == 1)
		printf("선택한 수는 %d 큰 수는 %d 입니다\n", check, upper(num1, num2, num3));
	else if (check == 2)
		printf("선택한 수는 %d 작은 수는 %d 입니다\n", check, lower(num1, num2, num3));
	else
		printf("잘못된 선택입니다\n");
		return 0;
}

//큰수 지정 함수
int upper(int num1, int num2, int num3)
{
	if (num1 > num2) //두 개 비교
		return (num1 > num3) ? num1 : num3; //나머지 비교
	else
		return (num2 > num3) ? num2 : num3;
}

//작은수 지정 함수
int lower(int num1, int num2, int num3)
{
	if (num1 > num2) //두 개 비교
		return (num2 > num3) ? num3 : num2; //나머지 비교
	else
		return (num1 > num3) ? num3 : num1;
}

//1와 2 둘중 어느 값이 왔는지 들어왔는지 체크
int checker(check)
{
	if (check>0)
		return 1;
	else
		return 0;
}
```



**문제2:** 

섭씨온도를 입력하면 화씨온도로 변환하는 <u>CelToFah이라는 함수</u>와

그 반대로 화씨 온도를 입력하면 섭씨를 반환하는 <u>FahToCel</u>이라는 

이름의 함수를 정의하고 호출하는 예제를 완성하자.

<u>Fal=1.8 X cel +32</u>



```c
double CelToFah(double c) //실수형 섭씨 -> 화씨
{
	return 1.8 * c + 32;
}
double FahTocel(double f) // 실수형 화씨 -> 섭씨
{
	return (f - 32) / 1.8;
}

int main(void)
{
	int num;
	double num2;
	printf("1.섭씨를 화씨로 2.화씨를 섭씨로 \n");
	scanf("%d", &num);

	if (num == 1)
	{
		printf("섭씨를 입력해주세요: \n");
		scanf("%lf", &num2);
		printf("변환된 화씨는 %f 입니다 \n", CelToFah(num2));
	}
	else if (num == 2)
	{
		printf("화씨를 입력해주세요: \n");
		scanf("%lf", &num2);
		printf("변환된 섭씨는 %f 입니다 \n", FahTocel(num2));
	}
	else
		printf("잘못된 선택입니다\n");

	return 0;
}
```



**문제3:**

인자로 전달된 수 만큼의 피보나치 수열을 출력하는 함수를 정의하자.

5를 입력시 0에서부터 시작해서 5개의 피보나치 수열을 출력한다.



```c
void Fibo(int num) //피노나치 수열
{
	int n1 = 0, n2 = 1, n3, n;
	if (num == 1)
		printf("%d", n1);
	else
		printf("%d %d ", n1, n2);

	for (n = 0; n < num - 2; n++)//0시작 / 입력한수-2까지 / 1증가
	{
		n3 = n1 + n2; //n3 = 앞두개 +
		printf("%d ", n3);
		n1 = n2; 
		n2 = n3; // 0 1 1 2 3
	}
}

int main(void)
{
	int num;
	printf("출력하려는 피보나치 개열 수: ");
	scanf("%d", &num);
	if (num < 1)
	{
		printf("피보나치는 1부터 가능합니다 \n");
		return -1;
	}
	Fibo(num);
	return 0;
}
```



## 지역변수

함수 내에서만 존재 및 접근 가능한 것을 지역변수라 한다.

중괄호 {} 내에 선언되는 변수는 모두 지역변수다.



```c
int SimpleFuncOne(void)
{
	int num = 10;     // 이후부터 SimpleFuncOne의 num 유효 = 지역변수 
	num++;
	printf("SimpleFuncOne num: %d \n", num);
	return 0;     // SimpleFuncOne의 num 유효한 마지막 문장
}

int SimpleFuncTwo(void)
{
	int num1 = 20;     // 이후부터 num1 유효
	int num2 = 30;     // 이후부터 num2 유효
	num1++, num2--;
	printf("num1 & num2: %d %d \n", num1, num2);
	return 0;     // num1, num2 유효한 마지막 문장
}

int main(void)
{
	int num = 17;     // 이후부터 main의 num 유효
	SimpleFuncOne();
	SimpleFuncTwo();
	printf("main num: %d \n", num);
	return 0;     // main의 num이 유효한 마지막 문장
}
```

이름이 같은 변수를 볼 수 있는데

지역변수는 중괄호 내에서만 영향을 끼치기 때문에 문제 없다.

지역변수는 휘발성처럼 해당 지역을 벗어나면 자동으로 소멸한다.



지역변수를 stack메모리 영역에 할당된다.

main -> Funcone => Functwo -> main

[main] -> [main Funcone] => [main Funone Functwo] => [main]이다.



즉 SimpleFunOne이 열번 호출된다고해서 변수가 10번 할당되는게 아니라

휘발되고 할당 휘발되고 할당의 반복이다.



#### 다양한 형태의 지역변수

지역변수는 반복문이나 조건문에도 선언이 가능하다.

```c
int main(void)
{
	int cnt; //count 
	for (cnt = 0; cnt < 3; cnt++)
	{
		int num = 0; //지역변수
		num++;
		printf("%d번째 반복, 지역변수 num은 %d. \n", cnt + 1, num);
	}

	if (cnt == 3)
	{
		int num = 7;
		num++;
		printf("if문 내에 존재하는 지역변수 num은 %d. \n", num);
	}
	return 0;
}
```

for문안에 지역변수가 있는데 이러면 반복되는 동안 누적일까?

아니다. 위에 말한것과 같이 휘발 되고 할당의 반복이다.



하지만 반복문내 변수선언은 되도록 지양하자.



```c
int main(void)
{
	int num = 1; //지역변수 1 (1)

	if (num == 1)
	{
		int num = 7;	   //주석과 미주석 차이 (2)
		num += 10;
		printf("if문 내 지역변수 num: %d \n", num);//(2)
	}
	printf("main 함수 내 지역변수 num: %d \n", num); //(1)
	return 0;
}
```

if문 내에서는 main에 있는 num이 가려지기 때문에

실행하면 지역변수가 달라진다.



**지역변수의 일종의 매개변수다.**

매개변수의 조건은

- 선언된 함수 내에서만 접근이 가능

- 선언된 함수가 반환시 지역변수와 마찬가지로 소멸된다.



지역변수의 큰 테두리안에 매개변수가 있다는 느낌이다.



## 전역변수

전역변수는 이름처럼 전역에 접근가능한 변수로서 중괄호 내에 선언되지 않는 특징이 있다.

```c
void Add(int val);
int num;    // 전역변수는 기본 0으로 초기화됨

int main(void)
{
	printf("num: %d \n", num);
	Add(3);
	printf("num: %d \n", num);
	num++; //전역변수 num 영향
	printf("num: %d \n", num);
	return 0;
}

void Add(int val)
{
	num += val;
}
```

`int num;`이 아무런 중괄호에 들어가지 않았는데 이는 전역변수이다.

- 프로그램 시작과 동시에 메모리 공간에 할당되어 종료 시 까지 존재
- 초기화를 하지 않으면 0이 디폴트
- 전체영역 어디든 접근이 가능



#### 전역변수와 동일한 이름의 지역변수가 선언되면?

"해당 지역의 전역변수는 가려지고, 지역변수의 접근이 이루어진다."

우선권이 지역변수 > 전역변수 라는 것이다.

```c
int Add(int val);
int num = 1; //전역변수

int main(void)
{
	int num = 5; //지역변수
	printf("num: %d \n", Add(3)); //add 진행
	printf("num: %d \n", num + 9); // 지역값 +9
	return 0;
}

int Add(int val)
{
	int num = 9;
	num += val;
	return num;
}
```

하지만 변수의 이름은 되도록 중복이 되지않게하자.



추가적으로, 전역변수는 최대한 적게 사용하는 것이 좋다.

전역변수는 많은 기능이 배포되어 있기 때문에, 수정하면 할 것이 많아지고 유지보수가 힘들다.

즉 프로그램이 복잡도가 높아지고 좋은 구조가 아니게 되기 때문.



#### 지역변수에 static 선언을 추가해서 만드는 static변수

static선언이 들어가면 전역변수를 지역변수로 만들어버리는 것이다.

```c
void SimpleFunc(void)
{
	static int num1 = 0; //전역변수의 static를 사용하여 안으로 넣음 초기화 0
	int num2 = 0;
	num1++, num2++;
	printf("static: %d, local: %d \n", num1, num2);
}

int main(void)
{
	int i;
	for (i = 0; i < 3; i++)
		SimpleFunc(); //얘가 호출하면 static은 보이지 않는다.
	return 0;
}
```

일단 전역변수랑 성격이 같다.

초기화 되지 않으면 0이고, 시작과 동시에 종료까지 할당된다.

하지만 static을 통해 해당 전역변수의 영향력을 지역변수처럼 만들 수 있다.



#### static 지역변수는 써도 되는가?

정답은 Yes다.

static지역변수는 전역변수로 쉽게 대체가 가능하기 때문이다.

전역변수의 단점을 static으로 어느정도 해결한셈이다.



#### register변수

오늘날에는 성능이 좋아져서 잘 사용하지 않는다고 한다.

CPU에는 ALU산술연산장치라는 것이 있어 그안에 레지스터가 있는데

레지스터에게

"나 이거 자주쓰니까 알아둬"정도만 귀띰해주는 것이다.



```c
int simple(void)
{
	register(int num = 3);
}
```

전역변수에는 register를 사용할 수 없으며,

허용해도 의미가 없다고 한다.





#### 문제 09-2 static변수 활용

```c
int total = 0;

int AddToTotal(int num)
{
	total += num;
	return total;
}
int main(void)
{
	int num, i;
	for (i = 0; i < 3; i++)
	{
		printf("입력%d: ", i + 1);
		scanf("%d", &num);
		printf("누적: %d \n", AddToTotal(num));
	}
	return 0;
}
//이 프로그램을 static으로 변환
```

이것을 보면 전역변수 int total을 사용한 것인데

이 전역변수는 AddToTotal에만 국한되어있는 것을 알 수 있어

그 안에 넣어주면 된다.

```c
int AddToTotal(int num)
{
	static int total = 0;
	total += num;
	return total;
}
int main(void)
{
	int num, i;
	for (i = 0; i < 3; i++)
	{
		printf("입력%d ", i + 1);
		scanf("%d", &num);
		printf("누적: %d \n", AddToTotal(num));
	}
	return 0;
}
```



## 재귀함수

재귀는 자기 자신을 다시 한번 호출하는 함수이다.



```c
void Recursive(void)
{
	printf("Recursive call! \n");
	Recursive( );
}
```

위에 Recusive함수가 있지만 그 안에 다시 Recursive를 부르게 되듯

자기 자신을 호출하는 것이다.



일단 완료되지 않아도 함수를 호출 할 수 있다.

함수를 다시 불러낸다는 개념보다는

"함수를 복사본을 만들어서 실행시킨다" 라는 개념이다.



#### 무한반복을 하면 안되니 탈출조건

```c
void Recursive(int num)
{
	if (num <= 0)
		return; //조건 탈출

	printf("Recursive call! %d \n", num);
	Recursive(num - 1);
}

int main(void)
{
	Recursive(3);
	return 0;
}
```

탈출 조건이 없으면 계속 복사만 하게 되니 탈출조건을 심어준다.

num값은 1씩 감소하되 0보다 작거나 같으면 탈출한다.



복사본 기준으로 생각하면

호출은 정방향이고 반환은 역반환이다.



#### 재귀함수의 사례

```c
팩토리얼값 n!=nx(n-1)... => n!=nx(n-1)!
```

팩토리얼 값을 반환하는 함수를 재귀적 구현



```c
if (n >= 1)
	return n * Factorial(n - 1);

if (n == 0)
	return 1;
else
	return n * Factorial(n - 1);
```

1이상이면 n x n(n-1)

0이면 1반환

그외는 n x n (n-1) 

3가지가 나오는데 이러면 2개로 묶기가 된다.

```c
if(n==0)
    return 1;
else
    return n*Factorial(n-1);
```





```c
int Factorial(int n)  //팩토리얼 진행 기능
{
	if (n == 0)
		return 1;
	else
		return n * Factorial(n - 1);
}

int main(void)
{
	printf("1! = %d \n", Factorial(1));
	printf("2! = %d \n", Factorial(2));
	printf("3! = %d \n", Factorial(3));
	printf("4! = %d \n", Factorial(4));
	printf("9! = %d \n", Factorial(9));
	return 0;
}
```





> 이렇게 이번에는 함수에 대해서 알아보았다
>
> 함수의 정의 ,재귀함수, 지역변수, 전역변수 등 기억하자