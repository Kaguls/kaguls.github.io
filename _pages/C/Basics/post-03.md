---

title: "[C언어의 기본] #3"
date: "2024-07-05"
thumbnail: "/assets/img/thumbnail/C.png"

---



# 반복실행을 명령하는 반복문

이제부터는 기본이 아니라 약간 응용의 영역이라고 한다. 시작해보자!



## while문에 의한 문장의 반복

반복문이란? : 문장을 열번 실행해주세요. 했을 때 문장을 열번 하는게 아닌 명령을 내리는 것

- 반복문의 종류) while문, do~while문, for문



일단 반복문은 많이 연습해서 머슬메모리처럼 몸이 반응되는 정도로 해야된다.

1.이해하기 : 예제중심으로 코드를 옮길 수 있을 정도로 이해

2.문제풀기 : 예제문제는 거의다 비슷하니까 문제제작해서 구현해보기



### while문은 반복을 명령하는 문장

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



### while문의 흐름

```c
int main(void)
{
    int num=0;
    while(num<3)
    {
        printf("Hi %d \n", num);
    }
}
```

















