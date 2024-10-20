---
title: "[C언어의 기본]포인터+함수"
date: "2024-10-19"
thumbnail: "/assets/img/thumbnail/C.png"
---

# 함수의 인자로 배열 정리

```c
int num;
fct (num);
// => fct함수에 num을 전달한다. ? => no. 복사한다에 가까움
//ㄴ 값이 복사가 되는 것.

int arr[3];
fct (arr[3]);
//=> 통째로 매개변수에 복사해서 전달하는 것인가?
//ㄴ 값이 복사가 되는 것.
//=> 통째로 매개변수를 복사해서 넣는 방법은 없음.


int arr[3];
fct (arr); //복사해서 매개변수에 넣어볼게

void fct(int arr[3]); //배열형태로 받을 수 있나?
//but C언어는 매개변수의 배열선언을 허용하지 않는다.
```

fct(num)은 int num의 값이 바뀌는 것이 아닌 값이 카피되어 나오는 것이다.

즉, 원래 값의 변화가 아닌 복사 값의 변화다.



두번째를 보면 

`int arr[3]` 선언 후 `fct(arr);`을 통해서 int arr[3]에는 접근이 불가능하다.

이는 컴퓨터에서 계획.txt파일을 복사 붙여넣기 한 후,

계획.txt(복사본)을 수정하는 것이기 때문에 원래 있던 계획.txt파일은 이상없다.



그러면 `void fct(int arr[3]);`은 되는가?

C언어는 매개변수의 배열선언을 허용하지 않기 때문에 불가능하다.



```c
int main 
{
	int age=10;
	fct (age); //함수 호출이 끝난 후 age 값이 +1 증가했으면 좋겠는데 가능? 불가능?
	// 불가능하다.
	//fct에 age를 넣는것이 불가능. 복사가 값이지 원래 age값의 조작은 불가능
	//fct는 복사본1로 노는 것이고 age파일은 무해함.
}

int age;
scanf("%d", &age); //접근가능 why? 주소값 이니까.


int age =20;
fct (&age);

void fct(int *ptr) //주소값을 가리키는 포인터
{
 *ptr+=1;
}
//이러면 age값은 증가한다. 
```

이 구문을 보면 알수있는 것은 위와 같이 복사본을 통해서 age값을 변할 수 없다는 것

하지만 scanf를 통한 코드를 보면 가능하다. 왜냐하면 & 주소값이기 떄문에.



그리고 배열선언이 아닌 void fct(int *ptr)로 선언하고 *ptr+=1을 하면

이는 주소값의 영역이기 때문에 age값은 증가한다.



### 인자전달의 기본방식

인자전달의 기본방식은 값의 복사다.

```c
int SimpleFunc(int num) {...}
int main(void)
{
	int age=17;
	SimpleFunc(age);
}
//age에 저장된 값이 매개변수 num에 복사가 됨. 17(복사본)
```

상단에 SimpleFunc을 선언 했다고 하고

main함수내에 int age선언후 이후 SimpleFunc를 통해서

main앞에서 int SimpleFun의 int num로 들어가는 순간

이때는 값의 복사를 통해서 들어간다는 것이다.



#### 배열을 함수로 인자를 전달하는 방식

```c
int arr[3]={1,2,3};
int * ptr = arr; //배열 arr은 int형 포인터다.

void SimpleFunc(int * param) {...}
//포인터 변수를 통해서 배열의 형태로 접근했음.
```

위처럼 배열을 선언 후

이에 대해서 배열 arr을 int형 포인터로 지정한다.

그 후 포인터 변수를 통해서 배열의 형태로 접근시킬 수 있다.

즉 , SimpleFunc의 매개변수는 int *param이 되어야한다.





```c
void ShowArayElem(int * param, int len) //계산 함수 len 배열의 길이
{
	int i;
	for(i=0; i<len; i++)
		printf("%d ", param[i]); //출력을 배열형태로 진행
	printf("\n");
}

int main(void)
{
	int arr1[3]={1, 2, 3};
	int arr2[5]={4, 5, 6, 7, 8};
	ShowArayElem(arr1, sizeof(arr1)/sizeof(int)); //arr1,4*3/4 
	ShowArayElem(arr2, sizeof(arr2)/sizeof(int)); //arr2,4*5/4
	//arr1 과 arr2는 길이가 다르지만 ShowArayElem 함수를 사용
	return 0;
}
// 123
// 45678
```

`void ShowArayElem(int * param, int len)`은 두번째 인자로 배열의 길이정보를 전달받도록 정의하였다.

`printf("%d ", param[i]);` 은  포인터 변수의 이름을 대상으로 배열형태의 접근을 진행하고 있다.

`ShowArayElem(arr1, sizeof(arr1)/sizeof(int)); `

`ShowArayElem(arr2, sizeof(arr2)/sizeof(int));`

이 두가지는 길이가 다른 두 배열을 대상으로 ShowArayElem함수를 호출한다.

arr1은 Int *param으로 포인터 값으로 전달, int len은 4x3/4로 = 개수 만큼 출력

arr2는 int *param으로 포인터 값으로 전달, int len은 4x5/4로 = 개수 만큼 출력

값을 출력해주게 되는 것이다.



```c
void ShowArayElem(int * param, int len)
{
	int i;
	for(i=0; i<len; i++)
		printf("%d ", param[i]);
	printf("\n");
}

void AddArayElem(int * param, int len, int add) //param에 arr[n]이 들어가는 것, ex) arr[n],3,1
{
	int i;
	for(i=0; i<len; i++)
		param[i] += add; //1씩 증가
}

int main(void)
{
	int arr[3]={1, 2, 3};
	AddArayElem(arr, sizeof(arr)/sizeof(int), 1); // 배열의 전체길이 / int의 길이 = 배열길이
	//주소값 전달, 배열길이, 1 전달하는 것
	ShowArayElem(arr, sizeof(arr)/sizeof(int)); //len이 3이 되서 올라감
	//param [0][1][2]가 234

	AddArayElem(arr, sizeof(arr)/sizeof(int), 2);
	ShowArayElem(arr, sizeof(arr)/sizeof(int));

	AddArayElem(arr, sizeof(arr)/sizeof(int), 3);
	ShowArayElem(arr, sizeof(arr)/sizeof(int));
	return 0;
}
```

이것은 위와 비슷한 구문으로, ShowArayElem과 AddArayElem함수 선언

그리고 메인함수 선언이다.



`int *param`에는 `arr[n]`값이 들어가게 된다.

그리고 각 len은 `sizeof(arr)/sizeof(type)`이다.



각 값을 함수에 넣으면 

```
2 3 4
4 5 6
7 8 9
```

가 출력된다.



`AddArayElem(arr, sizeof(arr)/sizeof(int), 1)` 가 진행되면

(주소값, 배열길이, 추가값)이 들어가는데, arr값이 순번대로 +1이 출력되면서 2,3,4의 출력이

`AddArayElem(arr, sizeof(arr)/sizeof(int), 2)`가 진행되면

기존 2,3,4출력에 +2로 출력된다.

이렇게 되는 코드다.



> 처음에 있듯
>
> int * ea = int ea[]이다.



그러면 위에

```c
void AddArayElem(int * param, int len, int add)
void ShowArayElem(int * param, int len)
//이 예제를 대신하여
void AddArayElem(int param[], int len, int add)
void ShowArayElem(int param[], int len)
//도 가능하다.
```

포인터를 배열의 이름으로 사용하는 것이 가능하듯!

```c
int arr[3]={1,2,3};
int * ptr =arr; 
```

그러면 이것은 될까?

int ptr[]=arr로 대체불가능하다.

왜냐하면 이것은 매개변수가 아니기 때문이다.



## Call-by-Value vs Call-by-reference

```c
int num=10;
fct (num);

fct(int *ptr)
{
	*ptr+=1;
}
```

위에서 배웠듯 위 같은 코드가 있다면 num값은 변하는가?

맞다. 왜냐면 주소값 *ptr를 썻기 떄문이다.



여기서 Call-by-value는 말그래도 값에 관한것이다. `fct(10);`

Call-by-reference는 참조에 관한것으로 `&num, *ptr`과 같은 주소 선언이다.



즉 우리가 지금까지 선언한 것의 대부분은 Value이다.



#### Reference 예시

```c
void ShowArayElem(int * param, int len) //주소값
{
	int i;
	for(i=0; i<len; i++)
		printf("%d","parm[i]);
	printf("\n");
```

int *param을 통해서 값의 변경시 원래 값도 변경되는 점을 알 수 있다.



```c
void Swap(int n1, int n2) //swap함수를 통해서 n1과 n2를 변경하기를 원함
{
	int temp=n1; //임시 저장소 temp
	n1=n2;
	n2=temp;
	printf("n1 n2: %d %d \n", n1, n2);
	//temp <- n1 <- n2 <- temp
}

int main(void)
{
	int num1=10;
	int num2=20;
	printf("num1 num2: %d %d \n", num1, num2);

	Swap(num1, num2);     // num1과 num2에 저장된 값이 서로 바뀌길 기대!
	printf("num1 num2: %d %d \n", num1, num2);
	return 0;
}
```

이러한 경우는 어떨까?

최종 결과값은 num1=20 , num2=10으로 나오지만 값 자체는 바뀌지 않는다. 

왜냐하면 Call-by-Value기 때문에 값의 복사가 일어나서

원래의 값은 영향을 주지 않기 때문이다.



#### 주소값을 전달하는 호출 Reference

```c
void Swap(int * ptr1, int * ptr2) //위와 다르게 포인터를 사용 (이는 주소를 향해있음)
{
	int temp = *ptr1;
	*ptr1 = *ptr2;
	*ptr2 = temp;
}

int main(void)
{
	int num1=10;
	int num2=20;
	printf("num1 num2: %d %d \n", num1, num2);

	Swap(&num1, &num2);     // num1과 num2에 저장된 값이 서로 바뀌길 기대!
	printf("num1 num2: %d %d \n", num1, num2);
	return 0;
}
```

위와 같은 예시는 ptr에 포인터를 통해서 주소값을 전달하기 떄문에

main함수의 값도 바뀌게 된다.



과거 우리가 scanf함수에 &붙히는 이유를 알 수 있다.

```c
int main(void)
{
	int num;
	scanf("%d",&num); //변수 num의 주소값을 scanf함수에 전달 
	//scanf의 할당받은 값을 전해주기 위해서 복사가 아니라 커넥트
}
```



그러면 str과 같은 문자열을 받을 때는 왜 주소값을 사용하지 않는가?

```c
int main(void)
{
	char str[30];
	scanf("%s",str); //&str는 잘못됨
}
```

반복했다싶이, 문자열 그 자체가 주소값이기 때문에 주소 주소값이 되어버려서 불가능하다.



### 문제풀이

```
문제1: 변수 num에 저장된 값의 제곱을 제공하는 함수정의
이를 호출하는 main함수를 작성해보자.
두가지 형태 valuve, reference로 한다.
```

```c
//Call-by-value
int squared_value(int num)
{
	return num * num; //제곱
}

//Call-by-referencec
void squared_reference(int* ptr)
{
	int num = *ptr;
	*ptr = num * num;
}

int main(void)
{
	int num = 2;
	printf("%d \n", squared_value(num));
	squared_reference(&num);
	printf("%d\n", num);
	//두줄로 나누어서 한다면 void형 함수인 reference부분이 값반환은 없으나
	//num변수 값을 변경하는 효과만 나오게 됨.
	
	//printf("%d\n", squared_reference(&num)); //불가능
	//void형 이기 때문에 호출 결과를 얻는 값이 없음.
	//컴퓨터에게 "아무것도 없는 것"을 출력해

	return 0;

}
```

간단한 주석은 넣었으나 추가적으로 설명하면 일단 Value은 자체값이라서 주소값이 없이 제작하고

Reference는 주소값이 있게 제작한다.

그후 main 함수에 함수를 이용한 출력을 넣어준다.



만약 `printf("%d\n", squared_reference(&num));`은 가능할까?

불가능하다. why? void형이기 때문에 호출 결과를 얻는 값이 없다.

즉 컴퓨터에게 아무것도 아닌 것을 출력해.라고 하는거다



```
문제2:세 변수 저장된 값이 서로 바뀌는 함수를 정의하자.
함수는 swap3 swap3(&num1,&num2,&num3); 느낌이다.
num1은 2에 2는 3에게 3은 1에게
```

```c
void swap(int* ptr1, int* ptr2, int* ptr3)
{
	int temp = *ptr3;
	*ptr3 = *ptr2;
	*ptr2 = *ptr1;
	*ptr1 = temp;
}

int main(void)
{
	int num1 = 1, num2 = 2, num3 = 3;
	swap(&num1, &num2, &num3);
	printf("%d %d %d\n", num1, num2, num3);
	return 0;
}
*/
```

서로 바뀌는 함수 swap을 통해서 꼬리물기처럼 한바퀴 돌아준다.

그리고 swap에는 주소값으로 묶어야되기에 맞춰준다.

그리고 출력하면 서로바뀌게 된다.



## 포인터 대상의 상수(const)선언

```c
Const + int * ptr
ptr -> num을 가리킴

//num이 상수화 되는 것인가?
//ptr이 상수화 되는 것인가?
```

이럴 때 num이 상수화인가? ptr이 상수화인가?



#### 포인터변수가 참조대상 변경허락하지 않는 상수화

```c
int main(void)
const int * ptr = &num;
*ptr =30; //컴파일 실패
num=40; //컴파일 성공
```

포인터 변수 ptr을 이용하여 ptr이 가리키는 변수에 저장된 값의 변경을 허용하지 않음.

즉, Const선언은 값을 변경하는 방법에 제한을 두는 것으로서 상수로 만드는 것은 아니다.



#### 포인터 변수의 상수화

```c
int*const ptr = &num;
//이러면 ptr이 상수가 된다.
```



```c
int main(void)
{
	int num1=20;
	int num2=30;
	int * const ptr=&num1;
	ptr=&num2; //컴파일 에러
	*ptr=40; //컴파일 성공
```

ptr이 상수고 ptr이 가리키는 대상 값은 상수가 아니라서 변경이 가능하다.



> 내 생각은 Const ( ) *ptr이면 const 뒤에 *까지 있으니 *ptr 불가능
>
> \* Const ptr이면 const뒤에 ptr만 있으니 ptr 불가능
>
> 즉 가리키는 값의 불변이냐, 포인터 자체의 불변이냐



### 만약 두개가 붙는다면?

```c
const int * const ptr = &num;
```

내 추측이 맞다면 이런경우 *ptr과 ptr둘다 값의 불변이 일어난다.

*ptr=20; 시도시 에러가 나올 것이고 ptr=&age여도 에러가 나올 것이다.



가리키는 값의 변경이 불가능하거 ptr자체도 다른주소를 가리킬 수 없기 떄문에



> 그러면 const선언은 어떤 의미가?
>
> const 선언은 생각보다 중요한데, 코드의 안전성을 높혀주는 것에 있다.

```c
int main(void)
{
	double PI=3.1415;
	double rad;
	PI=3.07; //실수의 문장이 삽입되면?
	scanf("%lf", &rad); //double형이라 lf
	printf("circle area %f \n", rad*rad*PI);
}
```

위와 같은 경우 실행이 된다. 하지만 문제가 발생한다.

PI의 값이 변경되지만 컴파일러는 이상이 없다고 판단하는거다.



```c
int main(void)
{
	const double PI=3.1415;
	double rad;
	PI=3.07; //컴파일 시 상수 값의 변동으로 오류 발생
	scanf("%lf", &rad); //double형이라 lf
	printf("circle area %f \n", rad*rad*PI);
}
```

Const선언이 된 경우 doulbe이 상수화되어 추후 PI값이 들어와도 오류가 발생한다.

즉 코드에 대한 안전성이 올라가는 것이다.



### 문제풀이 Const선언 이해

```
문제1: 아래 정의된 함수를 참고하여
인자로 전달되는 정보를 참조하여 int형 배열요소 전체를 출력하는 함수이다.
매개변수 arr을 대상으로 const 선언을 한 이유는?
```

```c
void ShowAllData(const int * arr, int len)  // const *arr 고정주소 , len 길이
{
	int i; //int i지정
	for(i=0; i<len; i++) //조건문 i 0부터 시작해서 i가 len보다 작을때 반복, i 1씩 증가한다)
		printf("%d", arr[i]); //arr[0] ~ 배열길이까지
}
```

이 코드를 보면 출력 arr[i]는 전체배열을 출력하는 함수다.

Const를 앞에 붙히는 이유는 *arr을 통해서 주소값 자체를 변하지 않게 하는 것이다.

배열 요소 값의 변동이 있는 경우를 제한하여 코드 변동을 확인할 수 있게 된다.



```
문제2: 예제를 보면 한 가지 지적할 사항이 있는데 그것이 무엇인가?
```

```c
void ShowData(const int* ptr) // *ptr에 const선언이 붙음 ptr이 가리키는 변수 저장된 값 변경 x
{
	int* rptr = ptr; 
	printf("&d\n", *rptr);
	*rptr = 20;
}

int main(void)
{
	int num = 10;
	int* ptr = &num;
	ShowData(ptr);
	return 0;
}
```

*rptr을 이용해서 ptr을 가리키는 변수값을 바꾸려고 하지만

ShowData함수에서 const int * ptr의 선언으로 값을 바꿀 수가 없다.



#### 정리

`const int* ptr` = ptr이 가리키는 값이 상수다.

즉 ptr을 통해서 가리키는 메모리 영역에 저장된 값은 변경이 불가능하다.

ptr 자체는 변경이 가능하다.



`int * const ptr` = ptr 자체가 상수다.

ptr이 가리키는 메모리 영역은 변경이 불가능하나 가리키는 값은 가능하다.



포인터관련은 끝이고 다음은 문제풀이로 만나도록 하겠다!
