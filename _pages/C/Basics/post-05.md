---
title: "[C언어의 기본]-도전프로그래밍1 문제풀이"
date: "2024-07-23"
thumbnail: "/assets/img/thumbnail/C.png"


---

# 도전 프로그래밍!

지금까지의 지식을 테스트해보고 예제문제를 풀어보는 시간이다.



## 문제1

10진수 정수를 입력받아서 16진수로 출력하는 프로그램을 작성해보자



```c
int main(void)
{
	int num;

	printf("10진수 입력해주세요:  ");
	scanf("%d", &num);

	printf("10진수  %d는 16진수 %x입니다. ", num, num);
}
```

10진수를 입력받아서 %d를 %x로 바꾼다.



## 문제2

두 개의 정수를 입력받아 구구단 출력하는 프로그램
조건 - 3과 5입력시 3 4 5단만 2와 4를 입력시 2 3 4만 출력된다.
조건 - 3 5, 5 3 순서에 관계없이 그 사이 범주의 값을 출력한다.



```c
//구구단 테스트 코드 작성
int main(void) {

	int dan1 = 2;
	int dan2 = 5;


	// 구구단 출력
	for (dan1; dan1 <= dan2; dan1++) {
		for (int num = 1; num <= 9; num++) {
			printf("%dx%d = %d\n", dan1, num, dan1 * num);
		}
		printf("\n");
	}

	return 0;
}

```

구구단의 기본적인 틀을 만들어 준다.



```c
int main(void)
{
	int mindan, maxdan, num= 0;
	int space = 0;

	printf("몇단부터 몇단을 출력하실건가요?: ");
	scanf("%d %d", &mindan, &maxdan);

	//무조건 작은수 앞 큰수 뒤
	if (mindan > maxdan) //min에 큰값이 max에 작은 값이 들어오면 변환
	{
		space = mindan; //공간에 큰 수 [5]
		mindan = maxdan; // min에 작은 값을
		maxdan = space; // 큰 공간에 큰수
	}

	//구구단 조건문
	//i=무조건 작은수 dan1, 조건 dan1이 dan2보다 크거나 작으면, i증가식
	for (mindan; mindan <= maxdan; mindan++) { //단의 증가
		for (int num = 1; num <= 9; num++) { //수가 1씩 증가하고 9까지 반복. 
			printf("%d x %d = %d\n", mindan, num, mindan * num);
		}
		printf("\n");
	}
	return 0;
}
```

`for (mindan; mindan <= maxdan; mindan++)` 를 보면

초기식 : mindan =0

조건식 : mindan <= maxdan (mindan이 maxn단보다 작거나 같을때까지)

증감식 : mindan ++ (mindan을 1씩 증가)



`for (int num = 1; num <= 9; num++)` 이거는 수다.

nx1 ~ nx9까지 출력하는 것이다.



## 문제3

두 개의 정수를 입력받아 최대공약수(GCD -greatest common divisor)를 구하자

추가로, 여유가 되면 유클리드 호제법을 조사하여 구현해보자.



```c
int main(void)
{
	int num1, num2;
	int gcd;
	int i; //기준 값

	printf("두개의 정수: ");
	scanf("%d %d", &num1, &num2);

	for (i = 1; i <= num1 && i <= num2;i++) //기준 i를 1부터 시작하여 늘려가는 나눗셈 반복
	{
		if (num1 % i == 0 && num2 % i == 0) //num1과 num2를 i로 나눠서 0이 나오는 값이 나오면
			gcd = i; //gcd에 i값을 넣어준다,
	}

	printf("%d와 %d의 최대공약수는 %d입니다 \n", num1, num2, gcd);

	return 0;
}
```

최대 공약수는 둘이 가지는 약수 중 가장 큰수



`for (i = 1; i <= num1 && i <= num2;i++)` 

초기식 : i를 기준 1부터 시작

조건식: i가 num1보다 작거나 같되, num2보다 작거나 같아야된다.

증감식: i증가



`if (num1 % i == 0 && num2 % i == 0)`

만약에 위 조건이 성립하고

i 나 눴을 때 나머지 값이 둘다 0이면 출력한다.





**유클리드 호제법 (최적화)**

두 개의 정수 혹은 다수의 자연수에서 최대공약수를 구하는 알고리즘
원리: 두 수가 서로 나눠서 나머지를 구하기. - 나머지 0이면 최대공역수



```
ex)168, 1980의 GCD
1980 / 168 = 168 * 11 + 132
168 /132 = 132 * 1 + 36
132/36 = 36 *3 +24
36/24 = 24 * 1 + 12
24/12 = 12 * 2 + 0 //나머지 0일때
12 = 최대공약수
1980 168의 문제를 24 ,12로 바꾸는 것이다.
```

```
a,b의 최대공약수 = (a,b):
a=bq+r  ex)a=4 b=2 q=2 r=0  => (a,b) = (b,r)
```

```
이 식에 168 1980 / 12 24를 보면
1980 / 168 = 168 * 11 + 132 = (1980[a],168(b), 11[q] + r[132])
```

```
a = bq+r => (a,b) = (b,r)
	=> 1980 = 168 * 11+132 => (1980,168) = (168,132)
	=> (168,132) ... (b,r)이 (a,b)위치로 가게되고 더 작은 수로 줄이는 과정
```



```c
//유클리드 구현 (반복문)

int gcd(int a, int b) //최대공약수 기능
{
	while(1) //항상 실행 loop - a와 b의 반복 교환
	{
		int temp = b; //b값은 계속 써야되니까 임시저장소
		b = a % b; // a와 b를 나눈 값을 b에 저장
		a = temp; // temp에 저장된 값을 a에 저장 (a,b)갱신

		if (b == 0) //b가 0이되면 최대 공약수가 생기니
			break; //탈출조건
	}
	return a; //값을 a값을 반환한다.
}

int main(void)
{
	int a, b;

	printf("두 수를 입력해주세요 : ");
	scanf("%d %d", &a, &b);

	printf("최대공약수는 %d", gcd(a, b)); //출력한다 gcd로 a와 b값을 한것
	return 0;
}
```

반복문이 된다면 결국 자기 자신을 호출하는 재귀함수도 된다고 생각해서 제작해봤다.



```c
//유클리드 구현(재귀함수)
int gcd(int a, int b) //최대공약수 기능
{
	if (b == 0) //상위조건 b가 0이면 
		return a; // a값을 반환한다.
	else //재귀조건 
		return gcd(b, a % b); //계속 자기를 호출시킴 (재귀)
	//b를 현재 값을 넣어주고, a%b를 하여 나머지를 구한다 = (b,r)
	//재 호출 후 (b,r)...반복하여 0까지 반복
}

int main(void)
{
	int a, b;
	printf("두 수를 입력해주세요 : ");
	scanf("%d %d", &a, &b);

	printf("최대공약수는 %d", gcd(a, b)); //출력한다 gcd로 a와 b값을 한것
	return 0;
}
```

재귀함수를 쓰면 반복문보다 코드도 짧고 편해지는 것 같다.



## 문제4:

도전4: 금요일 집으로 가는길 수중 5000원있음.
조건1; DVD한편을 빌림 - 수중 3500원
조건2: 크림빵500원, 새우깡700원 콜라400원 사려함.
무잔돈 + 최소 1개이상 구매
수중의 돈 3500, 500 700 400 최소1회로 0원조건



```c
int main(void)
{
	int money; //돈
	int bread = 500; //빵
	int shrimp = 700; //새우
	int cork = 400;  //콜라
	int a, b, c; //a-빵 b-새우 c-콜라

	printf("수중의 돈: ");
	scanf("%d", &money);

	for (a = 1; a < money / bread; a++) //빵을 1개부터 떨어질때까지 반복
	{
		for (b = 1; b < money / shrimp; b++) //새우를 1개부터 떨어질까지 반복
		{
			for (c = 1; c < money / cork; c++) //콜라를 1개부터 떨어질때까지 반복
			{
				if (bread * a + shrimp * b + cork * c == money) //이 조건을 출력 돈과 같은 경우
					printf("크림빵 %d개, 새우깡 %d개, 콜라 %d개 입니다\n", a, b, c);
			}
		}
	}
	printf("위 테이블이 가능한 수 입니다.");
	return 0;
}
```

모든 경우의 수 출력이다. 

변수를 아에 나누는 거로 하면 복잡하려나



```c
int main(void)
{
	int money; //돈
	int bread, shrimp, cork;
	int a, b, c; //a-빵 b-새우 c-콜라
	
	printf("수중의 돈: ");
	scanf("%d", &money);

	bread = money / 500;
	shrimp = money / 700;
	cork = money / 400;

	for (a = 1; a < bread; a++) //빵을 1개부터 떨어질때까지 반복
	{
		for (b = 1; b < shrimp; b++) //새우를 1개부터 떨어질까지 반복
		{
			for (c = 1; c < cork; c++) //콜라를 1개부터 떨어질때까지 반복
			{
				if (500 * a + 700 * b + 400 * c == money) //이 조건을 출력 돈과 같은 경우
					printf("크림빵 %d개, 새우깡 %d개, 콜라 %d개 입니다\n", a, b, c);
			}
		}
	}
	printf("위 테이블이 가능한 수 입니다.");
	return 0;
}
```

개인적으로 위 코드가 더 직관적인 것 같다..





## 문제5:

10개의 소수를 출력하는 프로그램
나눠서 (1, n) 이면 소수 / (1, n, 의외 수)가 있으면 소수가 아님



```c
int main(void)
{
	int num; //증가변수
	int i; //반복문 
	int count = 0; //개수 제한

	for (num = 2; count < 10; num++) //개수 증가 반복문 (0과 1은 소수가 아니여서 2부터)
	{
		for (i = 2; i <= num; i++) //1은 모든게 나뉘어져서 2로 제한, i가 num보다 작같
		{
			if (i == num) // i값과 num값이 같아지는 조건이면 소수다. i n만 인증
			{
				printf("%d ", num); 
				count++;
			}
			if (num % i == 0) //num과 i값의 나머지가 0이면 1 n +@이라 빠져나감.
				break; //탈출 다음 num값 이동 
		}
	}
	printf("\n");
	return 0;
}
```

최소 조건을 안해서 조금 애먹었다..

`for (num = 2; count < 10; num++)` 이 부분의 2

`for (i = 2; i <= num; i++)` 여기서 2

조금 고생했다..





## 도전 6:

초를 입력받으면 시 분 초 형태로 출력

```c
int main(void)
{
	int second;
	int h, m, s;

	printf("초 입력: ");
	scanf("%d", &second); //초 입력

	h = second / 3600; //3600나눈것
	m = (second%3600) / 60; //3600으로 나눈 것의 60나눈것
	s = (second%3600) % 60; //3600으로 나눈 것의 60나눈것의 나머지

	printf("입력 한 초는 %d이며 이는 %d시간 %d분 %d초 입니다", second, h, m, s);
	return 0;
}
```



초입력이라서 맨 처음에는 그냥 

```
3600s = 1h => /3600

60s = 1m => /60

s = n
```

으로 생각해서 짰는데 안됐다.



생각해보니 

1시간으로 나누고.

남은 값의 분

의 남은 값의 초다.



```c
h = second / 3600; //3600나눈것
m = (second%3600) / 60; //3600으로 나눈 것의 60나눈것
s = (second%3600) % 60; //3600으로 나눈 것의 60나눈것의 나머지
```

그래서 이렇게 정의했다. 



## 도전 7:

n을 입력받는다. 그리고 공식이 성립하는 k의 최대값을 계산하여 출력
$$
2^k <= n
$$
즉 내가 입력한 값에 2의 제곱 값이 나오는 것이다.



```c
int main(void)
{
	int n; //입력값
	int k; //k값
	int result = 1; //누적값

	printf("입력 값: ");
	scanf("%d", &n);

	for (k = 0; result <= n; k++) //k를 0부터 / 누적값이 n과 같아질때까지 K증가
		result *= 2; //2의 제곱 누적 result *2 = result 
	printf("k의 최대값은 %d \n", k - 1); //for가 커지면 종료되는데, k값은 넘은 값이니 -1 2^n-1

	return 0;
}
```

내가 256을 입력하면 k값은 8이 반환되어야 하는 거다.



`for (k = 0; result <= n; k++)` 

초기식: K=0

조건식: 누적값이 n보다 작거나 같을때까지

증감식 : K를 증가시킨다.



맞으면 result에 2배씩 누적된다.

2 * 1  =2 *2 = 4 *2 = 8...



출력에서 k-1을 해줘야한다.

왜냐면 for반복문에서 result값이 커지면 반복문이 종료된다.

즉 값이 이미 커져있기 떄문에 k값을 한 단계 내려주는 것이다.





## 도전8:

2의 n함수의 재귀 구현 - 위는 반복문이니 충분히 가능할 것이다.



```c
int recursion(int num) //재귀함수
{
	if (num == 1) //값이 1이면
		return 2; //2반환 2^1
	else //아니면 재귀걸기
		return 2 * recursion(num - 1); //2*(직전2^n) 값 출력
}

int main(void)
{
	int num; 
	printf("정수: ");
	scanf("%d", &num);
	printf("2의 %d승은 %d \n", num, recursion(num));
	return 0;
}
```

1이면 그냥 2를 뱉어주고 아니면

2*(재귀(num-1))을 해준다.



ex) 3이 입력되면 2*(3-1)이다.

왜냐면 재귀를 하면서 앞에 2*가 있으니 -1을 해주는 것이다.



솔직히 처음에 감이 잘 안왔다

자꾸 2배 큰 숫자가 나와서.. 근데 앞에 2를 곱해줘야되니 2를 뺴야되는 것이다.



```c
//재귀미사용
int answer(int);//기능 선언만 먼저

int main(void)
{
	int num;

	printf("정수를 입력해주세요: ");
	scanf("%d", &num);
	printf("2의 %d승은 %d \n", num, answer(num)); //재귀가 아니라서 num-1불필요
	//2의 정수승은 answer(정수)값

	return 0;
}

int answer(int a) //기능 출력은 int형
{
	int i; //제곱 변수
	int result = 1; //누적 변수

	for (i = 1; i <= a; i++) //1시작, a값보다 작같, i증감
		result *= 2; //2제곱 누적 i=1 2/ i=2 4/ i=3 6.. 누적
	return result; //결과값은 result값
}
```

for문으로 누적을 시켜주는데 재귀처럼 2를 시작하고 하는게 아니라서

` *=2`로 그냥 누적만 시켜주면 된다



>기본 적인 것이 끝나고 포인트와 배열로 간다!