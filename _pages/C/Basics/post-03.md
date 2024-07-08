---

title: "[C언어의 기본] #3"
date: "2024-07-05"
thumbnail: "/assets/img/thumbnail/C.png"

---



# 반복실행을 명령하는 반복문

이제부터는 기본이 아니라 약간 응용의 영역이라고 한다. 시작해보자!



# while문에 의한 문장의 반복

반복문이란? : 문장을 열번 실행해주세요. 했을 때 문장을 열번 하는게 아닌 명령을 내리는 것

- 반복문의 종류) while문, do~while문, for문



일단 반복문은 많이 연습해서 머슬메모리처럼 몸이 반응되는 정도로 해야된다.

1.이해하기 : 예제중심으로 코드를 옮길 수 있을 정도로 이해

2.문제풀기 : 예제문제는 거의다 비슷하니까 문제제작해서 구현해보기



## while문은 반복을 명령하는 문장

```c
while(num<3) //while(조건)
{
    printf("Hello world! \n");
    num++;
}
```

while문을 선언 후 괄호 안에 조건을 적어낸다. 

그러면 조건만큼 반복된다.

여기서는 Hello World 출력 후 num값을 1올려준 후 num값이 3보다 작을때 까지 반복한다.



```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
int main(void) //출력은 int + main함수 + 입력은 void
{
	int num = 0; //int형 변수 num 선언 및 0으로 초기화

	while (num < 5) // while ~동안 (조건) => 조건이 유지되는 동안 반복한다. 여기서는 num값이 5보다 작으면 반복 5보다 크거나 같으면 중단
	{
		printf("Hello world! %d \n", num); // 조건이 참 True가 반환될 경우 위 값을 수행한다.
		num++; // num ++이기때문에 num +1을 하는데 이 행을 벗어날 때 num값을 +1을 한다.
	}
	return 0;
}
```

num값은 0부터 시작하여 while문을 방문하여 조건 확인 후 True면 printf문 실행 후 num++을 하여 다시 while문으로 향하면서 num값에 +1을 해준다.

만약에 여기서 num++가 없으면 무한으로 반복된다. '무한루프'가 구동되는 것이다.



반복문에서 중요한 것은 **반복 조건을 무너뜨리는 최소한의 연산**이다.



### 반복의 대상이 하나의 문장이면 괄호는 생략이 가능

```c
while(num<5)
    printf("Hi %d \n", num++);
```

값의 라인이 한 개 있을 때는 생략이 가능하다는 것이며 하지만 오히려 줄인다고 해서 좋은건 아닌 듯하다.

가독성도 하나의 고려사항이라서..



## while문의 흐름

```c
int main(void)
{
    int num=0;
    while(num<3)
    {
        printf("Hi %d \n", num);
        num++;
    }
    ...
}
```

순서를 보면 순차적으로 내려오면서 변수 num이 0으로 초기화 된 후

반복문 while에 진입하게 되며 조건인 num값이 3보다 작기에 Hi를 출력하고 num값을 출력

그리고 num값이 +1이 되고 다시 while로 올라가면서 num값이 +1이 된다.

그리고 다시 반복문에 들어가서 반복된다.

num이 3이 되면 조건 불충분으로 반복하지 않고 밑으로 내려간다.



```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
int main(void) 
{
	int dan=0, num=1;
    printf("몇 단을 출력하나요?: ");
    scanf("%d", &dan);
    
    while(num<10)
    {
        printf("%dx%d=%d \n", dan, num, dan*num);
        num++;
    }
    return 0;
}
```

이것은 내가 만약 구구단 5단을 보고싶으면 5을 입력하면 

dan 변수에 내가 입력한 값으로 주소 대입



num은 초기화 된 1값부터 9가 될때까지 반복하는 조건이다.

그 안에는 반복이 되면 5단x 1~9 = 5*1~9 출력이 된다.



이는 순서도가 있지만 여기서는 삽입하지 않도록 하겠다.



### 무한루프

```c
while (1) //항상 True
{
    printf("%dx%d=%d \n", dan, num, dan*num);
    num++;
}
```

while(조건)에 1값인 True를 넣어주게 되면

이 조건은 항상 True가 되어 무한으로 반복되는 상황이 나온다.



이럴때는 break; 문을 통하여 빠져나갈 수 있고

특정기능을 사용하기 위해서 일부러 무한루프를 사용하는 경우가 있다고 한다.



## while문 연습 문제

#### 1.프로그램 사용자로부터 양의 정수 하나를 받아 그 수만큼을 "Hello world"를 출력하는 프로그램의 제작

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int num; //변수 num 입력받는 정보를 선언
	int standard = 0; // 변수 0 기준이되는 변수 standard 변수를 선언

	printf("정수를 입력해주세요. \n");
	scanf("%d", &num);

	while (standard<num) //5를 입력하면 5보다 작은 경우 출력 조건식은 0을 기준으로 0<5다.
	{
		printf("Hello world!\n"); //반복명령 Hello World를 출력한다.
		standard++; //1회 반복후 다시 while로 들어가면서 standard 변수에 +1을 해준다.
	}
	return 0;
}
```



#### 2.프로그램 사용자로부터 양의 정수를 하나 입력 받은 후, 그 수 만큼의 3의 배수를 출력하는 프로그램을 작성하라.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int num=0; //양의 정수를 입력받는 값
	int dan=0; //3의 배수를 출력해야되니 3단인 dan변수 지정 및 1초기화

	printf("정수를 입력해주세요\n"); //입력받을 변수 요청 출력
	scanf("%d", &num); //입력받은 변수를 num으로

	while (dan++ < num) //조건문 dan은 이행 후 1이 증가함. num보다 작은 조건 반복
	{
		printf("%d\n", 3 * dan); // 출력한다. 3*dan의 수만큼 1부터 시작.
	}
	return 0;
}
```

변수 num와 dan을 초기화 시켜준 후 정수를 입력받는다. 그 후 그 값을 num 값에 대입

반복문을 실행한다. 조건문에서 dan은 조건문을 이행 후 1이 증가하고 num보다 작은 조건을 반복한다.

 dan은 1부터 시작한다. 왜냐하면 dan++에서 printf로 넘어가면 1이 증가하기 때문이다.

3*dan을 해준다 (3의배수)



그러면 3*내가 입력한 정수의 숫자만큼 출력이 된다.

아마 이쪽은 num과 dan값이 0이니

```c
int num, dan=0;
```

으로 한줄을 더 줄일 수 있을 것이다.



```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int num = 0; //양의 정수를 입력받는 값
	int dan = 1; //3의 배수를 출력해야되니 3단인 dan변수 지정 및 1초기화

	printf("정수를 입력해주세요\n"); //입력받을 변수 요청 출력
	scanf("%d", &num); //입력받은 변수를 num으로 저장하는데 &num+1을 하면 num변수 주소에 +1을 더한값으로 메모리 위치가 아닌 다른 메모리 위치에 저장되어 있다.
	//그래서 변수 자체의 주소를 넘거야 하기 때문에 &num+1을 하기 보다는 하단 while 조건문의 num+1을 해준다.

	while (dan < num +1) //dan보다 num이 크다는 조건
	{
		printf("%d\n", 3 * dan); // 출력한다. 3*dan의 수만큼 1부터 시작.
		dan++; //dan이 1씩 증가되어감.
	}
	return 0;
}
```

입력받은 정수를 num값을 대입.



반복문을 실행하는데 조건은 dan보다 num+1이 클때까지

dan은 1씩 증가한다.



내가 3을 입력하면 dan은 1 num은 4기준으로 반복문이 진행된다.

즉 1~3이니 3번을 3*dan을 실행하기에 3 6 9 가 된다.



#### 3.프로그램 사용자로부터 계속해서 정수를 입력 받는다. 그리고 그 값을 계속해서 더해 나간다. 이러한 작업은 사용자가 0을 입력할 때 까지 계속되며 0을 입력하면 입력된 모든 정수의 합을 출력하고 종료한다.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int all=0;
	int num=1;

	while (num != 0)
	{
		printf("정수를 입력해주세요(0이 나오면 종료합니다)\n");
		scanf("%d", &num);
		all += num;
	}

	printf("입력된 수의 합은 : %d \n", all);
	return 0;
}
```

변수를 선언 후 

조건문에서 num!=0 변수 num가 0이 아닐때 까지 반복한다.



while문안에 scanf가 있기 때문에 반복되고 all이라는 변수에 누적된다.



```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int all = 0; //합을 저장할 수 있는 변수
	int num = 0; //입력받는 값의 수
	int num2 = 0; //수를 담는 그릇

	printf("더하고자 하는 값의 수를 입력하세요 \n");
	scanf("%d", &num);

	int i = 1; //반복 변수 지정
	while (i <= num)
	{
		printf("%d번째 수를 입력해주세요: ", i);
		scanf("%d", &num2);
		all += num2; // 변수 all에 num2의 값을 더하고 그 값을 다시 all에 저장하는 것이다. all = all + num2. 
		i++; 
	}

	printf("입력된 수의 합은: %d \n", all);
	return 0;
}
```

비효율적인거 같지만 내가 수를 지정해서 저장하는 것을 한번 해봤다.

변수 all, num, num2를 지정하고 내가 더하고자 하는 값의 수를 입력한다.



반복변수를 넣어 while문에 내가 더하고자하는 값만큼 반복한다. 

내가 더하고자한 값은 num2에 들어가고 all에 누적된 후 반복 변수가 1증가한다.



#### 4.프로그램 사용자로부터 입력 받은 숫자에 해당하는 구구단을 출력하되, 역순으로 출력하는 프로그램을 작성해보자.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int num = 9;
	int dan = 0;

	printf("구구단 몇단을 출력하실건가요?\n");
	scanf("%d", &dan);

	while (num > 0)
	{
		printf("%d x %d = %d\n", dan, num, dan * num);
		num--;
	}
	return 0;
}
```

num 변수를 9로 초기화하고, dan을 0으로 초기화한 후

내가 출력하고자 하고 싶은 구구단의 단을 입력하면 dan에 입력



반복문이 실행되며 조건은 num값이 0보다 클때다.

(dan) * (num) = dan *num 이 반복출력되며 1회 반복할때마다 num값은 1씩 줄어든다



#### 5.프로그램 사용자로부터 입력 받은 정수의 평균을 출력하는 프로그램을 작성하되 다음 두 가지 조건을 만족한다.

"먼저 몇개의 정수를 입력할 것인지 묻고 그 수만큼 입력받는다."

"평균 값은 소수점 이하까지 계산하여 출력한다"

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int ea = 0; //입력받는 정수의 갯수
	int num = 0; //정수의 입력
	int all = 0; //모든 정수의 입력을 담는 그릇
	int i = 1; //반복변수

	printf("입력받을 정수의 개수를 입력해주세요 \n");
	scanf("%d", &ea);

	while (i < ea+1)
	{
		printf("%d 번째 정수를 입력해주세요 \n", i);
		scanf("%d", &num);
		i++;
		all += num; //입력받은 모든 값을 all에 더해준다.
	}
	printf("입력받은 정수의 평균은 : %f \n", (double)all / ea); 
	return 0;
}
```

각각 변수들을 선언해준다. 

그 후 내가 입력받을 정수의 개수를 입력 해준 후

갯수만큼 반복되며 모든 값을 all에 저장된다.

마지막에 평균값을 출력하는데 소수점 까지 출력해야되니까

int형인 all을 double 실수형으로 바꿔준 후 갯수만큼 나눠준다. 그후 출력 %f을 해준다.



## while문의 중첩

while문의 중첩은 말 그대로 while문안에 마트료시카처럼 while문이 있는거다. 

즉, 조건 반복 안에 조건 반복이 있는것이다.



2단부터 9단까지 출력하는데 반복문 중첩이 없으면 반복문을 8회 삽입해야되니 비효율적이다.

즉 중첩을 시키면 짧게 할 수 있다. (최적화가 좋다)

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int cur = 2;
	int is = 0;

	while (cur < 10) //cur2부터 시작해서 9까지 반복 총 8회 반복한다.
	{
		is = 1; //새로운 단의 시작 is선언
		while (is < 10) //is 1부터 9까지 9회반복
		{
			printf("%dx%d=%d \n", cur, is, cur * is); //출력한다. nxm=nm이다. n=2->9 , m=1~9, n*m
			is++; //프린트 출력후 이 행을 벗어나면 is에 +1 다시 is=2로 간다.
		}
		cur++; //is가 10이 되면 cur +1을 진행하고 다시 9행으로 간다.
	}
	return 0;  //이 행은 총 cur 8 * is 9 = 72개의 답을 얻을 수 있다.
} 
```

cur2를 통해서 2단부터 시작한다. is는 0으로 초기화한다.

while문에서 큰 조건은 cur이 2부터 시작하여 9까지 반복을 하는것이니 2~9 => 8회 반복한다.

그  사이에 is=1;로 새로운 단의 시작을 적고

그 다음에 작은 조건 is가 10미만까지 반복이니 1~9까지 9회반복을 해준다.

is 9회 반복의 내용은 cur * is = cur *is를 9회 반복 해준 후

나가서 is가 10이 되면 빠져나와 cur이 1증가하는데 while(cur<10)으로 올라가면서

수가 1 증가한다.



그러면 총 cur 8 * is 9 = 72ea 답을 얻을 수 있다.



## while문의 중첩 문제

#### 프로그램 사용자로부터 총 5개의 정수를 입력 받아서, 그 수의 합을 출력하는 프로그램을 작성해보자.

조건!: 정수는 반드시 1 이상이어야한다. 1미만의 수가 입력되면 이를 인정하지 않고 재 입력을 요구한다. 

결과적으로 1이상의 정수를 5개를 모두 입력 받아야한다.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void) //while문의 중첩문
{
	int num = 0; //입력받는 정수의 값을 받을 변수
	int sum = 0; //합을 출력하는 변수
	int ea = 0; //입력받는 변수의 수를 받는 변수

	while (ea < 5) //개수가 0~4 즉 5개가 될때까지 반복한다.
	{
		while (num <= 0) //입력받는 변수가 0보다 작거나 같을때 반복한다. 즉 1미만의 수를 입력시 반복되는 구간
		{
			printf("입력받을 정수 (%d번째)\n", ea + 1); //입력받을 정수 EA+1번째
			scanf("%d", &num); //num변수 주소저장
		} //1미만이 들어오면 여기서 계속 루프된다.
		sum += num; //sum= sum+num
		num = 0; // num=0; 
		ea++; //여기까지 완료시 ea+1
	}
	printf("모든 값의 합은 : %d \n", sum);
	return 0;
}
```

각 변수들을 0으로 초기화해준 후 

반복문을 실행하는데 

대반복문(ea<5) 0~4로 즉 5개가 될때까지 반복하게 된다.

소반복문(Num값이 0보다 작거나 같을 때 반복한다.) = 1미만 정수 입력 시

[만약 1미만이 들어오면 while문에서 안에서 계속 반복되기에 빠져나갈 수 없다.]

소 반복문을 통해서 정수를 입력받고 그것을 num으로 받아 sum에 누적시킨다.

그 후 num값을 0으로 초기화 (기록삭제)

그후 ea의 값을 한개 늘려준다. 

그후 ea값이 4까지 반복해준다. 



 ```c
 #define _CRT_SECURE_NO_WARNINGS
 #include<stdio.h>
 
 int main(void) //while의 중첩문 나의 방식
 {
 	int num = 0; //받은 정수값
 	int sum = 0; //합의 정수값
 	int ea = 0; //받은개수의 정수값
 	int is = 0; //시작 개수의 정수값
 
 	while (ea <= 0) //입력받을 정수 값이 1미만일 경우 루프 생성
 	{
 		printf("입력받을 정수의 개수를 입력해주세요");
 		scanf("%d", &ea);
 	} 
 	
 	while (is < ea) // 0~n까지 내가 입력받은 정수만큼 반복
 	{
 		while (num <= 0) //입력받은 정수값이 1미만시 루프생성
 		{
 			printf("정수 값을 입력해주세요. (%d번째의 입력)\n", is + 1); //%d에 is+1번째 입력을 통해 몇번째인지 확인가능
 			scanf("%d", &num); //입력받은 값을 num에 저장
 		} //만약 1미만시 다시 while문으로 아니면 아래로 진행한다.
 		sum += num; //sum=sum+num 총합의 값을 저장한다.
 		num = 0; //저장된 num값을 초기화 시켜준다. 초기화 안하면 루프 값 유지됨.
 		is++; //정수값을 +1해준다.
 	}
 	printf("입력받은 정수는 %d개 이며, 총합은 %d 입니다.", ea, sum);
 	return 0;
 }
 ```

변수를 4개 지정해준다. C언어는 순차적으로 실행되니

일단 1차 while문으로 정수 값이 1미만 이었을 떄의 루프를 먼저 생성해준다.

내가 입력하고 싶은 정수의 개수를 입력하되 1미만은 불가능



그후 새로운 반복문으로 내가 입력받은 정수반복 반복시킨다.

그 내부 반복문에는 내가 더하고자 하는 값이 1미만일때 반복을 시킨다.

내부 반복문이 반복되면서 sum에 정수 값을 누적 및

num의 초기화 밑 횟수+1을 해주며 입력받은 정수의 수만큼 반복한다.



그 후 입력받은 정수의 개수와 총합을 보여준다.



#### 아래의 출력으로 보이는 프로그램을 작성해보자

```
*
ㅇ*
ㅇㅇ*
ㅇㅇㅇ*
ㅇㅇㅇㅇ*
```

참고로 5행에 걸쳐 출력이 이뤄지며, 행이 더해질때마다 ㅇ의 문자수가 증가한다.



```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int star_ea = 0;
	int o_ea = 0;

	while (star_ea < 5) //별의 갯수가 5개 이하면 반복한다.
	{
		while (o_ea < star_ea) //별의 개수보다 o의 개수가 적으면 반복한다. 
		//맨 첨은 0<0이 성립이 되지 않으니 while문 바로 종료
		{
			printf("o"); // o을 출력
			o_ea++; // o갯수를 ++해준다.
		}
		o_ea = 0; //o갯수를 초기화 
		printf("* \n"); //별의 출력
		star_ea++; //별 개수 카운트 1늘려준다.
	}
	return 0;
}
```



변수로 별의 개수 즉, 5행이니까 <5를 조건을 걸어준다. 별의 개수가 5개 이하면 반복 [ 0,1,2,3,4]

소 반복문에는 별의 개수보다 o이 적으면 반복하는 것이다. 

맨 처음은 0=0이기에 바로 종료 후 *을 한개 출력 그후는 0<1이니 ㅇ이 한개 앞에 추가 되어 반복된다.

그러면 문제와 같은 답이 도출된다.

```C
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int star_ea = 0;
	int o_ea = 0;
	int ea = 0;

	printf("몇 층으로 올리실 건가요?\n");
	scanf("%d", &ea);

	while (star_ea < ea) //별의 개수가  ea만큼 반복한다.
	{
		while (o_ea < star_ea) //o의 개수보다 *의 개수가 더 적으면 실행한다.
		{
			printf("o"); //먼저 o를 출력
			o_ea++; //o값 +1
		} //o값+1했는데 도 *보다 작은지 체크
		o_ea = 0; //출력해준다.
		printf("* \n"); //*출력
		star_ea++; //star 카운트 +1
	}
	return 0;
}
```

요즘 응용해서 내가 원하는 층만큼 올려보는 거로 응용해봤다.

입력받은 층수만큼 별의 개수가 나올떄까지 반복하게 된다.



# do~ while문에 의한 문장의 반복

do ~while문은 while문과 다른점은 '반복조건'을 뒤에 작성하는 것이다.

즉, **무조건 최소 한번 이상은 실행되는 구조**다.



```c
do
{ 
    printf("Hello world! \n");
    num++;
}while(num<3);
```



일단 한번 실행 후 조건만큼 반복한다.



그러다보니 순서만 바꾼것인데 while문과 do while문으로 서로 교체할 수 있다.

```c
while(num<10)
{
    printf("%d x %d = %d \n",dan,num,dan*num);
    num++;
}
```

```c
do
{
    printf("%d x %d = %d \n",dan,num,dan*num);
	num++;
}while(num<10);
```

자세히 보면 거의 순서의 차이라고 볼 수 있다.



```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int total = 0, num = 0;

	do
	{
		printf("정수 입력(0 to Quit): ");
		scanf("%d", &num);
		total += num; //누적
	} while (num != 0);
	printf("합계 %d\n", total);
	return 0;
}
```

이것처럼 일단 한번 입력한 후에 앞으로 더 입력할 수 있을지 없는지 결정을 지어야되는 경우 같을 때

do~while이 필요하다.



## while문과 do~while문 문제

#### 일단 한번 받고 값을 더 받을건지 안받을건지 결정하는 문제를 기반으로 재 구현해보자

1. 변수 num값을 적절히 초기화해서 첫 번째 반복조건의 검사결과가 '참'이 되게 한다.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int total = 0, num = 1;

	while (num != 0) //num값이 0인지 아닌지 체크
	{
		printf("정수 입력(0 to Quit): ");
		scanf("%d", &num); //num값을 입력받음 주소 저장
		total += num;  //누적
	} //0이 아니면 반복 루프구간
	printf("합계 %d\n", total);
	return 0;
}
```

변수 total과 num을 각각 0과 1로 초기화 해준다.



while문으로 num값이 0인지 아닌지 체크해주고 0아니면 반복문을  계속 루프한다.

0이 나오면 끝나고 합계를 알려준다.



2. while문에 진입하기 전에 프로그램 사용자로부터 값을 1회 입력 받게 한다.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int total = 0, num = 0;

	printf("정수 입력하세요(0이면 종료): ");
	scanf("%d", &num);
	total += num; //0이면 최종값은 0으로 진행

	while (num != 0) // 0을 받으면 그냥 아래
	{
		printf("정수 입력하세요(0이면 종료): ");
		scanf("%d", &num);
		total += num;
	}
	printf("합계는: %d \n", total);
	return 0;
}
```

진입하기전에 일단 정수값을 받은 후 누적을 한번 시킨다.

그 후 입력 한 값이 0이면 누적값은 0으로 종료된다.

원래 코드가 do~ while이었는데 변경시키니 1회 입력이면 do ~while이 좋다는 것을 알았다.



#### 0이상 100이하의 정수 중에서 짝수의 합을 출력하는 프로그램을 구현해보자.

단 do~while 기반이어야 하며, 덧셈의 결과는 2550 이어야한다.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int num = 0;
	int sum = 0;

	do //일단 실행한다.
	{
		sum += num; // 0부터 누적값을 구하기
		num = num + 2; // num+2값을 해준다 0,2,4,....100
	} while (num <= 100); //100까지 반복한다.

	printf("합은 : %d \n", sum);
	return 0;
}
```

변수를 초기화 후 일단 한번 실행을 시켜준다.

0부터의 누적값을 구한 후 num+2를 통해 짝수를 선별한다.

그 값을 100까지 반복하고 합을 나타낸다.

```c
int main(void)
{
	int num = 0;
	int sum = 0;

	while (num <= 100)
	{
		sum += num; // 0부터 누적값을 구하기
		num = num + 2; // num+2값을 해준다 0,2,4,....100
	}
	printf("합은 : %d \n", sum);
	return 0;
}
```

do ~while을 while문으로 바꾸면 순서처럼 이렇게 바뀌게 된다. 굉장히 쉽다.



```c
int main(void)
{
	int sum = 0;//합을 받을 정수
	int start = 0;//시작 할 정수
	int end = 0;//종료할 정수

	printf("시작할 정수를 입력해주세요");
	scanf("%d",&start);
	
	printf("끝낼 정수를 입력해주세요");
	scanf("%d", &end);

	do
	{
		sum += start; //start부터 누적값 구하기
		if (start % 2 == 0) //start가 짝수일때
			start += 2; //start 값에 +2를 해준다.
		else start += 2; //아니면 start에 2씩 누적한다.
	} while (start <= end);
	printf("총 합은 %d입니다.\n", sum);
	return 0;
}
```

이번에는 내가 직접 범위를 지정하여 결과를 추출한다.

근데 모든 값이 2씩 누적이라 의미가 없는 것 같다.;



```c
int main(void)
{
	int sum = 0;
	int start = 0;
	int end = 0;
	char num[10];

	printf("시작 범위를 입력해주세요");
	scanf("%d", &start);

	printf("끝낼 범위를 입력해주세요");
	scanf("%d", &end);

	printf("짝수를 구할건가요?, 홀수를 구할건가요?: ");
	scanf("%s", num);

	if (strcmp(num, "짝수") == 0)
		printf("짝수로 인식되었습니다.\n");
	else if (strcmp(num, "홀수") == 0)
		printf("홀수로 인식되었습니다.\n");
	else
	{
		printf("값을 다시 확인하세요.");
	}

	int i = start;
	while (i <= end)
	{
		if (strcmp(num, "짝수") == 0)
		{
			while (i <= end && i % 2 == 0)
			{
				sum += i;
				i += 2;
			}
		}
		else if (strcmp(num, "홀수") == 0)
		{
			while (i <= end)
			{
				if (i % 2 != 0)
				{
					sum += i;
				}
				i++;
			}
		}
		else
		{
			printf("값을 다시 확인해주세요 \n");
			return 0;
		}
	}
	printf("%d ~ %d범위내에서 %s를 선택하여 총합은 %d입니다.\n", start, end, num, sum);
	return 0;
}
```

이번에는 위의 작품에서 범위를 나타내고 짝수와 홀수에 따라서 값이 다르게 했다.

범위를 입력 후 짝수와 홀수를 선택하며 짝수가 홀수가 아니면 값을 다시 확인하라는 문구가 뜨게한다.



새로운 변수에 시작 범위 값을 넣어주고 



짝수일시)그 값이 끝 범위보다 작거나 같고 2로 나눴을 때 0이 만족되면

start값을 누적시켜준다. 그후 +2를 더 누적시킨 후 끝 범위까지 반복한다.



홀수일시) 그 값이 끝 범위보다 작거나 같고 2로 나눴을 때 0이 아니면

start값을 누적시켜준다. 그후 +1를 더 누적시킨 후 끝 범위까지 반복한다



짝수도 홀수도 아니면 값을 다시 확인해달라고 안내가 뜨며 종료되고

조건이 만족하면 범위와 짝수홀수의 선택 그리고 총합을 보여준다.



#### while문의 중첩 예제를 do~while문으로 재구성해보자.

```c
#define _CRT_SECURE_NO_WARNINGS
#include<stdio.h>

int main(void)
{
	int cur = 2;
	int is = 0;

	do //while 자리에 do
	{
		is = 1; 
		do
		{
			printf("%dx%d=%d \n", cur, is, cur * is); //출력한다. nxm=nm이다. n=2->9 , m=1~9, n*m
			is++; //프린트 출력후 이 행을 벗어나면 is에 +1 다시 is=2로 간다.
		}while (is < 10) 
		cur++; //is가 10이 되면 cur +1을 진행하고 다시 9행으로 간다.
        printf("\n");
	}while(cur<10);
	return 0;  //이 행은 총 cur 8 * is 9 = 72개의 답을 얻을 수 있다.
} 
```

while문의 위치에 do가 오고 괄호 끝에 while(조건)을 넣어준다.



# for문에 의한 문장의 반복

일단 말하기 전에 반복문은 크게 2가지가 있다고 한다.

첫 번째, 횟수가 정해져 있는 상황. 

두 번째, 횟수가 정해지지 않은 상황 (조건)



for문은 while문을 편하게 쓰기위해 압축된 틀과 같다.



"Hi문자를 3회 출력하고 싶습니다."



```c
int main(void)
{
	int num = 0; //초기식
	while (num < 3)  //조건식
	{
		printf("Hi~");
		num++; //증감식
	}
	....
}
```

기존의 while문의 경우 우리는 이렇게 사용했다.

주석에 따라서 초기식 조건식 증감식이 있는데 이것을 그냥 for 형식의 틀에 맞게 옮겨주면 된다.



for (초기식; 조건식; 증감식)

```c
int maiint main(void)
{
	for (int num = 0; num < 3; num++)
		printf("Hi~");
}
```

이렇게 순서대로 넣으면 while문과 같게 된다. 가독성이 높아졌다.



1.int num=0 / 2=num <3 / 3.Printf() / 4.num++

가 있다면 1이후 2 3 4가 반복으로 이루어 진다는 것이다.



그러면 무조건 for문을 쓰는가? 그건 아니다.

반복의 횟수가 정해졌다면 for문이며 값을 기다리는 상황이면 while문이 더 자연스럽다.



### for문 기반의 다양한 예제

```c
int main(void)
{
	int total = 0;
	int i, num;
	printf("0부터 num까지의 덧셈, num은? ");
	scanf("%d", &num);

	for (i = 0; i < num + 1; i++) 
		total += i;

	printf("0부터 %d까지 덧셈결과: %d \n", num, total);
	return 0;
}
```

이렇게 하면 for문 덕분에 가독성이 올라가고 편하며 코드를 조금 더 줄일 수 있지만 두 가지 스타일을 익히자.



```c
for (int i=0; i<num +1; i++)
```

처럼 바뀔 수 있는 것이다. 초기화가 안에 들어가는 것



```c
int main(void)
{
	double total = 0.0;
	double input = 0.0;
	int num = 0;

	for( ; input>=0.0 ; )
	{
		total += input;
		printf("실수 입력(minus to quit) : ");
		scanf("%lf", &input);
		num++;
	}
	printf("평균: %f \n", total/(num - 1));
	return 0;
}
```

이 예제는 입력하는 실수의 평균값을 출력하며 작은 음의 실수 값이 입력될 떄 까지 계속되고 마지막 0은 제외한다.



여기서 자세히보면 초기식과 증감식이 없는데 진행되었다.! for문은 필요없다면 채우지 않아도 된다.

이때 조건문이 비어버리면 조건이 없어서 모든 값이 True가 된다.



```c
```



ex) for( ; ;) <- 처럼 말이다.



## 문제 for문의 활용

#### 프로그램 사용자로부터 두 개의 정수를 입력 받아, 두 정수를 포함하여 그 사이에 존재하는 정수들의 합을 계산하는 프로그램

단 두 번째 수가 더 커야 한다는 조건

```c
int main(void)
{
	int start1=0;
	int start2=0;
	int total=0;

	printf("두개의 정수를 입력해주세요: ");
	scanf("%d %d", &start1, &start2);

	for (total = 0; start1 <= start2; start1++)
		total += start1;

	printf("합계는 %d \n", total);
	return 0;

}
```

2개의 정수를 입력 받은 후,  누적값을 0으로 만든다.

그 후 start1 변수가 start보다 작거나 같은  때,

start이 1씩 커진 후 누적한다.



```c
int main(void)
{
	int start = 0;
	int end = 0;
	int total = 0;

	printf("두개의 정수를 입력해주세요: ");
	scanf("%d %d", &start, &end);

	if (start > end || start == end) //만약에 start가 end보다 크거나 같은 경우
	{
		int temp = start; //정수형 temp에 임시로 start값을 넣는다.
		start = end; //end를 start에 삽입한다.
		end = temp; //temp값을 end에 삽입한다.
	}
	//이를 통해서 교환이 이루어지는 코드가 완성되었다.

	for (total = 0; start <= end; start++)
		total += start;

	printf("합계는 %d \n", total);
	return 0;
}
```

추가 연습으로 만약 start 가 end보다 크다고 해도 여유공간을 통해 저글링 하듯 옮겼다.



#### 다음 수식인 계승(팩토리얼)을 계산하는 프로그램을 작성해보자

```c
n! = 1*2*3....*n;
```

이 수식에 맞는 프로그램을 작성해보자.



```c
int main(void)
{
	int start;
	int factorial;
	int multiplied=1;

	printf("입력 받고자하는 n!의 값을 입력해주세요: ");
	scanf("%d", &factorial);

	for (start=1; start <= factorial; start++)
		multiplied *= start ;

	printf("%d!은 %d입니다.\n", factorial, multiplied);
	return 0;
}
```

변수 초기화 후, 몇 팩토리얼을 할지 결정한다.



그후 start 가 팩토리얼보다 작거나 같을 때 까지 반복한다.

그리고 그 값을 누적으로 곱해준다.





## for문의 중첩

while문의 중첩처럼 for문에도 중첩을 할 수 있다.

```c
int main(void)
{
	int cur, is;

	for (cur = 2; cur < 10; cur++)
	{
		for (is = 1; is < 10; is++)
			printf("%dx%d=%d \n", cur, is, cur * is);
		printf("\n");
	}
	return 0;
}
```

구구단처럼 초기화 값과 범위에 의하여 2~ 9 *1~9 최대 81를 얻을 수 있다



```c
int main(void)
{
	int cur = 2;
	int is = 0;

	while (cur < 10)
	{
		int is = 1;
		while (is < 10)
		{
			printf("%dx%d=%d \n", cur, is, cur * is);
			is++;
		}
		cur++;
		printf("\n");
	}
	return 0;
}
```

그 값을 while문으로 바꾸면 초기식 조건식 증감식을 분활해주면 된다.



이렇듯 while, do~while, for에 대해서 배웠고,

반복문은 중요하니 자주 연습하고 꾸준히 해야겠다.!



# 조건적 실행과 흐름의 분기

흐름의 분기가 필요한 이유?

: 기존의 배운 계산기는 덧셈하고 뺄셈하고 곱셈하고 나눗셈을 했다면 이제는 선택을 하여 내가 필요한 것을 한다.



## if문을 이용한 조건적 실행

```c
if (num1 > num2) //num1이 num2보다 크다면 아래 조건문을 실행
{
	printf("A \n");
	pritnf("B \n");
}
```

if(조건) => 조건문의 내용이 True면 내용 문을 실행한다.

if문은 컴퓨터가 이렇게 써도 한줄로 이해한다. 컴파일러는 한 문장으로 이해하기 때문이다.



**우리가 if else문은 세로로 길게써도 컴파일러는 if ~ else 라고 보이는 거다.**



```c
int main(void)
{
	int num;
	printf("정수입력");
	scanf("%d", &num);

	if (num < 0)
		printf("0보다 작다\n");
	if (num > 0)
		printf("0보다 크다\n");
	if (num == 0)
		printf("0이다\n");

	return 0;
}
```

입력받은 num변수의 값의 조건에 따라서 출력되는 값이 다른 것이다.



num=1이라고 하면 첫 번째 (num<0)에서 False후 밑으로 간다.

(num>0)으로 간후 True로 printf문을 출력

(num == 0)으로 간후 false후 밑으로 간다.



```c
//계산기 프로그램

int main(void)
{
	int opt;
	double num1, num2;
	double result;

	printf("1.덧셈 2.뺄셈 3.곱셈 4.나눗셈 \n");
	printf("선택?");
	scanf("%d", &opt);
	printf("두 개의 실수입력: ");
	scanf("%lf %lf", &num1, &num2);

	if (opt == 1)
		result = num1 + num2;
	if (opt == 2)
		result = num1 - num2;
	if (opt == 3)
		result = num1 * num2;
	if (opt == 4)
		result = num1 / num2;

	printf("결과: %f \n", result);
	return 0;
}
```

이렇게 보면 좋은 것 같지만 문제점이 발생한다.

**if문이 모두 다 한번씩 거쳐간다는 점이다. 즉 이건 효율적이지 못하다..**



```c
//1~100범위 내 3의 공배수 또는 4의 공배수를 출력

int main(void)
{
	int num;

	for (num = 1; num < 100; num++)
	{
		if (num % 3 == 0 || num % 4 == 0) // || 연산자보다 == 연산자 우선순위가 높음
			//이러면 두개의 연산 결과에 대해서 ||연산을 수행
			printf("3또는 4의 배수: %d \n", num);
	}
	//이러면 {}를 없앨 수 있음 printf는 하나의 if문 이기 떄문이다.
	return 0;
}
```



## if ~else문을 이용한 흐름의 분기

```c
//if ~else문

if (num1 > num2) //참이면 아래 문 실행
{
	printf("num1이 num2보다 크다. \n");
	pritnf("%d > %d \n", num1, num2);
}
else //거짓이면 아래 문을 실행
{
	printf("num1이 num2보다 크지않다.\n");
	printf("%d <= %dn, num1, num2");
}
```

맨 처음에 말한 것처럼, if 문 1개 else 문 1개로 보이는게 아니라

if ~ else문 한개로 한 문장이다.



```c
int main(void)
{
	int num;
	printf("정수입력: ");
	scanf("%d", &num);

	if (num < 0)
		printf("입력 값은 0보다 작다\n");
	else
		printf("입력 값은 0보다 작지 않다\n");
}
```

값이 True면 if문 내의 printf값을 출력.

그 외 값은 else를 실행한다.



## if... else if... else의 구성

```c
if (조건1)

else if (조건2)

... (무한 조건n else if)

else (모든 조건 불만족)

조건 만족시 밑에 조건은 모두 무시한다.
```

기존의 if문과 다른 점은 else if에서 조건이 만족되면 밑의 else if문을 실행하지 않는다.



조건3이 만족한다는 기준)

if(조건1) false => else if(조건2) false => else if (조건3) True => 탈출



```c
//계산기 프로그램의 if..else if..else

int main(void)
{
	int opt;
	double num1, num2;
	double result;

	printf("1. 덧셈 2.뺄셈 3.곱셈 4.나눗셈 \n");
	printf("선택? ");
	scanf("%d", &opt);
	printf("두 개의 실수 입력: ");
	scanf("%lf %lf", &num1, &num2);

	if (opt == 1)
		result = num1 + num2;
	else if (opt == 2)
		result = num1 - num2;
	else if (opt == 3)
		result = num1 * num2;
	else if (opt == 4)
		result = num1 / num2;
	else
	{
		printf("1~4 사이의 값이 아닙니다.");
		exit(1);
	}


	printf("결과: %f \n", result);
	return 0;
```

기존의 계산기 프로그램은 if문을 모두 실행하였다.

하지만 else if문으로 건너뛰는 특성으로 인하여 연산의 수가 줄어들었다.





## if ... else if .. else의 진실

```c
if (num > 0)
	printf("A \n");
else if (num > 0)
	printf("B \n");
else
	printf("C \n")
```

```c
else  if (num>0)

else

	if (num>0) 
```

두 개를 비교하면 else if에 if else(IF else(if ...))인 것이다.



## 조건 연산자:  '삼 항 연산자'

if~else문의 대신으로 한 줄로 표현하는 문이다.

마치 n=n+m을 n+=M 같은 것이다.



(num1>num2) ? (num1) : (num2);



```c
int num3= (num1>num2) ? (num1) : (num2);
```

이런 조건식이 있다고 해보자.



변수 num3은 조건식(num1>num2)을 보고

True면 num3=num1

false면 num3=num2



**조건연산자는 코드를 간결하게 해준다.**



```c
int main(void)
{
	int num, abs;
	printf("정수 입력: ");
	scanf("%d", &num);
	
	abs = num > 0 ? num : num * (-1);
	printf("절댓값: %d \n", abs);
	return 0;
}
```

이것처럼 if ~ else문을 간략하게 뽑을 수 있다.



## 문제 if~else문의 활용

#### 첫 번째. 1이상 100미만의 정수 중에서 7의 배수와 9의 배수를 출력하는 프로그램 (단 7과 9의 공배수는 한번만 출력해야한다.)

조건체크 : 1이상 100미만의 정수 / 7의 배수 / 9의배수 / 7과 9의 공배수



```c
int main(void)
{
	int count;

	for (count = 1; count < 100; count++)
	{
		if (count % 7 == 0 || count % 9 == 0)
			printf("%d\n", count);
	}
	return 0;
}
```



추가. 만약에 7과 9의 공부새만 2번 출력하려면 어떻게 해야될까?

```c
int main(void)
{
	int count;
	int detection = 0 ; //7과 9의 공배수를 판별하는 함수

	for (count = 1; count < 100; count++)
	{
			if (count % 7 == 0 && count % 9 == 0) //최상위 조건 : 공배수 출력
			{
				printf("%d\n", count);
				printf("%d\n", count);
				detection = 1;
			}
			if (count % 7 == 0 && detection == 0)
				printf("%d\n", count);
			if (count % 9 == 0 && detection == 0)
				printf("%d\n", count);

			if (detection = 1 && count > 63)
			{
				if (count % 7 == 0)
					printf("%d\n", count);
				if (count % 9 == 0)
					printf("%d\n", count);
			}
	}
	return 0;
}
```

일단 먼저 7과 9의 공배수를 출력하는데 있어



```c
if (count % 7 == 0 && count % 9 == 0)
   {
	printf("%d\n", count);
	printf("%d\n", count);
	detection = 1;
	}
```

이 것을 삽입해주는데 2번 출력하는게 생각이 안나서 printf를 두 번 했다.

그리고 공배수가 나왔는지 안나왔는지 detection 변수를 통해 공배수가 나오면 1을 올려준다.



```c
if (count % 7 == 0 && detection == 0)
	printf("%d\n", count);
if (count % 9 == 0 && detection == 0)
	printf("%d\n", count);
```

일단 공배수가 7, 9이면서 공배수가 나오지 않는 AND조건으로 넣는다.



```c
if (detection = 1 && count > 63)
	{
	if (count % 7 == 0)
		printf("%d\n", count);
	if (count % 9 == 0)
		printf("%d\n", count);
	}
```

공배수가 한번 이상 출력되었으며, 63이상일때

7공배수 9공배수를 출력한다.



이게 없으면 63이후가 안나오기 때문에 추가했다.



#### 두 번째, 두 개의 정수를 받아 두 수의 차를 출력하는 프로그램을 구현해보자.

단, 무조건 큰 수에서 작은 수를 뺸 결과를 출력한다. 7 5면 2 , 5 7이여도 2다. 



조건: 두 개의 정수, 두 수의 차, 큰 수에서 작은 수 (작은 틀 한개 추가)

```c
int main(void)
{
	int num1, num2;
	int subtract;

	printf("두 개의 수를 입력 해주세요: ");
	scanf("%d %d", &num1, &num2);

	//subtract= (num1 - num2);
	if (num1 > num2)
		subtract = num1 - num2;

	else
		subtract = num2 - num1;
	
	printf("빼기 값은: %d 입니다 \n", subtract);
	return 0;
}
```

두 개의 수를 입력받아 num1이 크면 num1 -num2 아니면 num2 -num1다.



#### 세 번째, 학생의 전체 평균점수에 대한 학점을 출력하는 프로그램을 작성하자.

90점이상은 A, 80점 이상은 B, 70점 이상은 C, 50점 이상은 D 그리고 그 미만은 F.

순서대로 국, 영,수 점수를 받아 평균을 출력한다.



조건체크: 국영수점수, 평균점수, 학점별 조건

```c
int main(void)
{
	int language, english, math;
	double average;

	printf("순서대로 국어, 영어, 수학 점수를 입력해주세요: ");
	scanf("%d %d %d", &language, &english, &math);
	average = (language + english + math) / 3.0;
	printf("평균값은: %f \n", average);

	if (average >= 90.0)
		printf("학점: A");
	else if (average >= 80.0)
		printf("학점: B");
	else if (average >= 70.0)
		printf("학점: C");
	else if (average >= 60.0)
		printf("학점: D");
	else
		printf("재수강: F");
    
	return 0;
}
```

if ~ else if로 조건을 넣어준다.

조금 아쉬운건 excel의 count(범위)처럼 개수를 세듯

변수의 개수를 자동으로 세주는 함수가 있다면

```c
average = (language + english + math) / (변수 갯수 함수)
```

이렇게 하면 좀 더 좋을 것 같다. 



#### 네 번째, 위의 문제2  if ~else문을 이용해서 해결하면 그것을 조건 연산자로 변환해보자.

```c
int main(void)
{
	int num1, num2;
	int subtract;

	printf("두 개의 수를 입력 해주세요: ");
	scanf("%d %d", &num1, &num2);

	subtract = (num1<num2)? num2-num1: num1-num2;

	printf("빼기 값은: %d 입니다 \n", subtract);
	return 0;
}
```

if ~ else문이 간단해졌다.



# 반복문의 생략과 탈출

반복문인 (while, do~while, for)문에서 쓰는 것으로 continue와 break가 있다.

생략 continue / 탈출 break 다.



## Break 빠져나간다. 탈출

```c
int main(void)
{
	int sum = 0, num = 0;

	while (1) //항상 True
	{
		sum += num; //sum = sum+num
		if (sum > 5000) //sum이 5000이상이면 발동
			break; // 종료 (break는 자신을 감싸는 가장 가까운 위치 반복문 하나 빠져나감)
		num++; 
	}

	printf("sum: %d \n", sum); //sum =1+2+3...n 100까지 5050 99면 
	printf("num: %d \n", num); //num =숫자
	return 0;
}
```

위의 예제를 보면 break문을 통해서 if문을 빠져나올 수 있다!

if문이 실행되면 break가 실행되면서 if문이 바로 종료된다.



주의: if의 빠져나가는 것이 아닌, 가장 가까이 감싸는 반복문을 하나 탈출하는 것이다.



```c
결과값은 sum: 5050 num: 10
```

왜냐하면 sum값은 1+2+3...n

num값은 1+1+1+1...n



등차수열로 구해보자
$$
등차수열 
S_n=n(a_1+a_n)/2 이다.
$$

$$
S_n=100(1+100)/2 \\ =100*101/2 \\ =10100/2 \\5050
$$

즉 C언어로 등차수열을 구현한 것이다.





## continue 반복조건으로 되돌아가자. 생략

break문과 마찬가지로 반복문 안에 삽입이 되는데, 조건이 만족하면 그냥 뒤에 문장을 생략하고 반복문으로 가는 것이다.



```c
//컨티뉴 예제

int main(void)
{
	int num;
	printf("start! ");

	for (num = 1; num < 20; num++)
	{
		if (num % 2 == 0 || num % 3 == 0) //2의 배수 3의 배수는 
			continue; // 여기서 다시 위로 올려버림
		printf("%d", num); //2의 3의 배수는 작동x
	}
	printf("end! \n");
	return 0;
}
```

1~20 사이의 범위에서 2와 3의 배수가 아닌 것을 출력한다.

if문의 조건이 참이면 continue를 진행시켜서 밑을 생략하고 올리니 printf를 생략한다.



## 문제 continue &break 활용

#### 첫 번째. 구구단을 출력하되 짝수 단(2단 4단 6단 8단)만 출력되도록 하자.

추가로 2단은 2X2까지 4단은 4X4까지 6단은 6X6까지 8단은 8X8까지 출력되도록 만들자.



조건체크: 짝수 단을 출력 / 2단은 ... 8단은 8X8까지 출력

```c
int main(void)
{
	int dan;
	int su;

	for (dan = 1; dan < 10; dan++)
	{
		if (dan % 2 != 0)
			continue; //실행이 안되게 위로 올려 버리기

		for (su = 1; su < 10; su++)
		{
			if (su > dan)
				break;
			printf("%d x %d = %d 입니다\n", dan, su, dan * su);
		}
		printf("\n");
	}
	return 0;
}
```

일단 for문을 통해서 구구단의 큰 틀인 n단의 반복문을 만들어준다.

1조건을 넣는다 (짝수 단이면 출력 아니면 미출력) `if(dan&2!=0)` 이다.

그리고 작은 틀은 nXm에서 m단의 반복문을 만들어준다.

2조건을 넣는다 (2=2x2 4=4x4이니까 단x수로 보면 수는 단을 초월할 수없기에 `if(su>dan)`을 넣는다)





#### 두 번째, 다음 식을 만족하는 모든 A와 Z를 구하는 프로그램을 작성해보자.


$$
AZ\\
+ZA\\
-----\\
99
$$
 가능한 모든 수의 조합을 시도하기 위해 반복문을 조합한다.

```c
int main(void)
{
	int A, Z; // A와 Z 변수
	int sum; //A+Z의 합

	for (A = 0; A < 10; A++) //A는 0부터, 10이하, 1반복시 +1 A의 경우의 수대입
	{
		for (Z = 0; Z < 10; Z++) //Z는 0부터, 10이하, 1반복시+1 Z의 경우의 수 대입
		{
			if (A == Z) //A와 Z가 같다면 중복방지 
				continue; // 조건문으로 올려버린다. Z++후에 Z<10 진행 5+5 4+4는 불가능
			//없어도 실행과 값은 같은데 아마 연산의 차이가 나는 듯. 중복방지
			sum = (A * 10 + Z) + (Z * 10 + A); // (1~9*10+1~9)AZ + (1~9 * 10 + 1~9)ZA 경우의 수
			if (sum == 99) //sum이 99면 
				printf("%d%d+%d%d=%d\n", A, Z, Z, A, sum); //printf 출력
		}
	}
	return 0;
}
```

A를 1~9까지 범위에서 1증가 , Z 1~9까지 범위에서 1증가

그리고` if(A==Z) continue`로 중복을 방지해준다. 

AZ+ZA인 `sum = (A * 10 + Z) + (Z * 10 + A)`를 넣는다.



**만약) AB+BA=88이면**

```c
int main(void)
{
	int A, B;
	int sum;

	for (A = 0; A < 10; A++)
	{
		for (B = 0; B < 10; B++)
		{
			sum = (A * 10 + B) + (B * 10 + A);
			if (sum == 88)
				printf("%d%d+%d%d=%d\n", A, B, B, A, sum);
		}
	}
	return 0;
}
```

이렇게 처리할 수 있다. 근데 ` if(A==Z) continue`을 넣으면 44+44가 출력되지 않아서 제거했다.



**만약) 만약 ABC+DEF=999**

```c
int main(void)
{
	int A, B, C;
	int D, E, F;
	int sum;

	for (A = 0; A < 10; A++){
		for (B = 0; B < 10; B++){
			for (C = 0; C < 10; C++){
				for (D = 0; D < 10; D++) {
					for (E = 0; E < 10; E++) {
						for (F = 0; F < 10; F++) {
							sum = (A * 100 + B * 10 + C) + (D * 100 + E * 10 + F);
								if (sum == 999)
								printf("%d%d%d+%d%d%d=%d \n", A, B, C, D, E, F, sum);
						}
					}
				}
			}
		}

	}
	return 0;
}
```

for문안에 for문안에 for문안에.. ;;

이런 다중 중첩일때 중괄호를 들여쓰기 하면 오히려 가독성이 구려서 for 마지막에 넣어줬다.



# switch문에 의한 선택적 실행과 goto문



swtich문은 if...else if...else와 유사한 측면이 있다.

하지만 switch문은 if...else if..else문에 비해서 제한적이다.



## switch문의 구성과 기본기능

```c
int main(void)
{
	int num;
	printf("1이상 5이하의 정수입력: ");
	scanf("%d", &num);

	switch(num)
	{
	case 1: //case 1영역 1입력시 여기서부터 실행
		printf("1은 ONE\n"); 
		break;  //빠져나감! 근처의 반복문 switch 종료
	case 2:
		printf("2은 TWO\n");
		break;
	case 3:
		printf("3은 THREE\n");
		break;
	case 4:
		printf("4은 FOUR\n");
		break;
	case 5:
		printf("5은 FIVE\n");
		break;
	default:
		printf("I don't know! \n");
	}
	return 0;
}
```



내가 입력한 num값을 받아서 그것을 switch에 넣어서 그 값에 따라서 case문의 내용을 출력한다.

case문 내부에 break가 없으면 그 밑으로 쭉 실행으로 하는 것이고

break;가 존재시 거기까지만 진행된다.



switch(2)라고 하면 case 1 -> case 2로 가는 것이 아닌 한번에 case2로 간 후 실행되고 break문으로

가장 가까운 반복문 swtich를 탈출한다. break문이 없다면 2부터 쭈욱 실행된다.



#### switch문의 일반적 형태

```c
int main(void)
{
    ...
    switch(n)
    {
     case 1:
     printf("A1");
     pritnf("A2";
     break;
     case 2:
     printf("B1");
     pritnf("B2";
     break;
     default
     	printf("default");
    }
            ...
}
```

기본 적 형태로 n에 값에 따라서 내가 실행할 case영역이 다른 것이다.



## break문을 생략한 형태의 switch 문 구성

해당 case문만 실행되도록 switch문의 동작방식을 결정하면 일일히 break를 안달아도 된다.

```c
int main(void)
{
	char sel;//문자 받음
	printf("M 오전, A 사과, E 엘프 \n");
	printf("입력: ");
	scanf("%c", &sel);

	switch (sel)
	{
	case 'M':
	case 'm':
		printf("Morning \n");
		break;
	case 'A':
	case 'a':
		printf("Apple \n");
		break;
	case 'E':
	case 'e':
		printf("elf \n");
		break; //불필요한 break
	}
	return 0;
}
```

이번에는 기존과 다르게 char형 변수를 지정하여

내가 입력한 문자를 받아들여 출력하는데 대소문자에 대한 case를 부여하여 실행시킬 수 있게 한다.



**break문이 삽입되어서 유용한 경우가 있고 break문이 들어가지 않아서 유용한 경우가 있다.**



## switch vs if...else if..else

둘은 차이가 있다.

**"분기의 경우의 수가 많아지면 가급적 switch문으로 구현한다. - 가독성"**



```c
//if..else if..else

if (n == 1)
	printf("A");
else if (n == 2)
	printf("B");
else if (n == 3)
	printf("C");
else
	printf("D");
```

```c
//switch

switch (n) {
case 1:
	printf("A");
	break;
case 2:
	printf("B");
	break;
case 3:
	printf("C");
	break;
default
	printf("D");
}
```

switch문이 더 간결해보이는 것을 할 수있다.



실제로 if..else if..else문은 비선호한다고 하며

switch문을 선호하기에 switch문의 가독성 향상을 위한 코드를 작성하도록 노력해보자!



**"하지만 switch는 한계가 있다. 표현하기 애매하면 if ...else if ..else를 사용해야되는 것이다."**



```c
//if..else if..else

if (0<=n && n<10)
	printf("10");
else if (10 <= n && n < 20)
	printf("1020");
else if (20 <= n && n < 30)
	printf("2030");
else
	printf("40");
```

```c
switch (n) {
case ?:
	printf("10");
	break;
case ?:
	printf("20");
	break;
case ?:
	printf("30");
	break;
	default
		printf("40");
}
```

이렇게 보면 조건이 복잡하여 switch 문으로 표현하기 어렵다.

이런 경우에는 분기의 수가 많아도 switch문을 고집할 필요 없다.



## 문제 switch 문으로 변경하기

if...else if ...else문과 switch문은 서로 교체가 가능하듯 해보자!

```c
int main(void)
{
	int n;
	printf("0이상의 정수를 입력해주세요");
	scanf("%d", &n);

	switch (n/10) { //10을 나눠숴 0=1~9 / 1=10~19 / ...
	case 0: //값이 0이면
		printf("0이상 10미만입니다.");
		break;
	case 1: //값이 1이면
		printf("10이상 20미만입니다.");
		break;
	case 2:
		printf("20이상 30미만입니다.");
		break;
	default:
		printf("40이상 및 재입력");
	}
	return 0;
}
```

이렇게 조건을 잘 설정할 수 있으면 swtich!!



## 마지막으로 goto에 대해서 소개하자.

goto문은 마검과 같고, 실제로 잘 사용하지 않는다고한다.



```c
int main
{
	..
	rabbit:
	...
	goto rabbit;
	...
}
```

rabbit이라는 레이블을 지정하고 가다가 `goto rabbit`를 하면 rabbit으로 이동하는 것이다.



```c
int main(void)
{
	int num;
	printf("입력: ");
	scanf("%d", &num);

	if (num == 1)
		goto ONE;
	else if (num == 2)
		goto TWO;
	else
		goto OTHER;

ONE:
	printf("1입력\n");
	goto END;
TWO:
	printf("2입력\n");
	goto END;
OTHER:
	printf("다른 값\n");

END:
	return 0;
}
```

이러면 입력하는 것에 따라서 내가 설정한 레이블로 간다.



이러면 단점들이 보인다

첫 번째. 가독성이 구려진다 (왜냐? 점프하는 것으로 넘어가서 봐야되니까)

두 번째. 버그가 발생할 수 있다

세 번째. 절차저리의 역전이 발생한다.



=Joat다.



그냥 이런 것만 알고있고 쓰지말자.
