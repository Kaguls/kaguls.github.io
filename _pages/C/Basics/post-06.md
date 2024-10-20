---
title: "[C언어의 기본]배열 이해 선언 초기화"
date: "2024-10-18"
thumbnail: "/assets/img/thumbnail/C.png"
---

# 2챕터 배열

Visual studio 에서 직접 테스트 해보고 블로그에는 따로 안올려놔서 한번에 업로드 하게 될 것 같다.

원래 Visual Studio Code로 작성했는데 불편해서 타이포라로 바꾸니까 좀 많이 편해진 것 같다..

시작한다



## 배열

배열이란? 다수의 데이터를 처리하는 경우 유용하게 사용하는 것이다.

```c
int main(void)
{
	int floor101, floor102, floor103, floor104; //1층 101~104호
	int floor201, floor202, floor203, floor204; //2층 201~204호
}
```

예를 들어 위와같이 아파트의 층에 따른 구분과 호수에 따른 구분을 저장하는 예시인데

이렇게 저장하면 하나하나 다 기입해야되니까 별로다..



위처럼 1차원배열의 선언에는 3가지가 필요하다 : `배열이름, 자료형, 길이정보`이다.

`int onedimarr[4];` 이것은 자료형 / 변수이름/ 길이 의 순서로 입력된 것이다.

= int형 변수 4개로 이루어진 onedimarr배열이다. 이것은 int int int int 이다.



```c
int arr1[7]; //int형 1차원 배열 arr1 - 길이 7
float arr2[10]; //float 형 1차원 배열 arr2 - 길이 10
double arr3[12]; //double형 1차원 배열 arr3 - 길이 12
```

배열의 길이정보는 범용적 컴파일러를 위해서 상수로한다.

최근 새로운 C의 표준은 int len=20; int arr[len]이 가능하다.



### 선언된 1차별 배열의 접근

```c
int arr[3]; //길이3 int형 1차원 배열

arr[0] = 10; //배열  arr의 첫 번째 요소에 10 저장
arr[1] = 12; //배열 arr 두 번째 요소 12
arr[2] = 25; //배열 arr 세번 쨰요소 25

arr[idx] = 20; //배열 arr의 idx+1번째 요소에 20을 저장
```

설명은 주석으로 적어서 그렇고 

즉 arr[idx]의 기본형은 배열 의 idx+1번째 요소에 = n;값을 저장하는 것이다.



```c
int main(void)
{
	int arr[5];
	int sum = 0, i;

	arr[0] = 10, arr[1] = 20, arr[2] = 30, arr[3] = 40, arr[4] = 50;

	for (i = 0; i < 5; i++) //배열의 순차접근
		sum += arr[i];

	printf("배열요소에 저장된 값의 합: %d \n", sum);
	return 0;
}
```

이 구문을 통해 알수 있는 점은

배열의 모든 요소는 반복문을 이용하여 순차적인 접근이 가능하다는 것이다.



#### 배열의 선언과 동시에 초기화 설명

```c
int arr[5] = { 1,2,3,4,5 }; //순차적으로 1,2,3,4,5를 초기화함.

int arr[ ] = {1,2,3,4,5,6,7}; //이러면 자동으로 컴파일러에 의해서 7일 삽입됨.

int arr[5] = {1,2} 이러면 후방 요소는 0으로 채워짐 1 2 3 0 0 
```

배열에 들어가면 순차적으로 초기화 시키고 

빈 상태로 넣으면 컴파일러가 자동으로 삽입해줌

그리고 빈칸은 0으로 채워지게 됨.



```c
int main(void)
{
	int arr1[5] = { 1, 2, 3, 4, 5 }; //배열 1
	int arr2[] = { 1, 2, 3, 4, 5, 6, 7 }; //배열 2 7저장
	int arr3[5] = { 1, 2 }; //배열 3 후열 0저장
	int ar1Len, ar2Len, ar3Len, i; //기타 변수

	printf("배열 arr1의 크기: %d \n", sizeof(arr1)); //4byte *5
	printf("배열 arr2의 크기: %d \n", sizeof(arr2)); //4byte * 7
	printf("배열 arr3의 크기: %d \n", sizeof(arr3)); // 4byte * 5

	ar1Len = sizeof(arr1) / sizeof(int);     // 배열 arr1의 길이 계산 (EA) => 20/4 = 5개
	ar2Len = sizeof(arr2) / sizeof(int);     // 배열 arr2의 길이 계산 (EA) => 28/7 = 4
	ar3Len = sizeof(arr3) / sizeof(int);     // 배열 arr3의 길이 계산 (EA)

	for (i = 0; i < ar1Len; i++) //배열의 길이를 보는 반복문 5까지
		printf("%d ", arr1[i]);
	printf("\n");

	for (i = 0; i < ar2Len; i++) //7까지
		printf("%d ", arr2[i]);
	printf("\n");

	for (i = 0; i < ar3Len; i++) // 5까지
		printf("%d ", arr3[i]); 
	printf("\n");
	return 0;
}
```

이 문장을 보면 배열의 이름을 대상으로 하는 sizeof 연산의 결과는 바이트 단위의 배열의 크기이다.

`sizeof(arr1)/sizeof(int)`는 arr1의 size인 4byte *5 = 20개 에서 기본 인트 4byte를 나눈 5개를 출력



#### 문제풀이1

```
길이가 5인 int형 배열을 선언해서 프로그램 사용자에게 5개의 정수를 입력받자.
입력 종료시 다음의 내용을 출력하라
1.입력 정수 중 최대값 2. 입력 정수 중 최소값 3. 입력 정수의 총합
```



```
int main(void)
{
	int arr[5];
	int max, min, sum;
	int ea;

	//값 입력 반복문
	for (ea = 0; ea < 5; ea++)
	{
		printf("값을 입력하세요: ");
		scanf("%d", &arr[ea]);
	}

	//최대값
	max = min = sum = arr[0]; //배열변환
	for (ea = 1; ea < 5; ea++) //반복값
	{
		sum += arr[ea]; //sum변수 누적값
		if (max < arr[ea]) //만약 최대치보다 arr[ea]이 크면
			max = arr[ea]; //max값에 넣기 최대치 삽입
		if (min > arr[ea])
			min = arr[ea]; //min값에 최소치 삽입
	}

	printf("최대치: %d \n", max);
	printf("최소치: %d \n", min);
	printf("합계: %d \n", sum);
	return 0;
}
```



### 문제풀이 2

```
char형 1차원 배열을 선언과 동시에 다음 문장의 내용으로 초기화,
초기화후에는 저장된 내용 출력예제 "Good Time"
```



```c
int main(void)
{
	char ea[] = { 'G','o','o','d',' ','t','i','m','e' };
	int arrlen = sizeof(ea) / sizeof(char);
	int i;

	for (i = 0; i < arrlen; i++)
		printf("%c", ea[i]);
	printf("\n");
	return 0;

}
```

개수를 담은 다음에 그것을 i에 대입해서 반복문을 진행하여서

순차적 접근하여 실행한다.



## 배열을 이용한 문자열 변수표현

`char str[30]`=30보다 작은 ~ 것이다.

char형 배열의 문자열 저장과 널 문자를 알아보자



`char str[14] ="Good morning"`이라는 것이 있다고 치면

배열에는 Good morning+ \0가 저장이 된다.



왜냐하면 컴퓨터는 어디서 끝나는지 알아야되는데 그것을 찾는 조건이 \0이기 때문이다.

그래서 +1이 카운팅된다. 이것이 Null문자 라는 것이다.



```c
int main(void)
{
	char str[] = "Good morning!";
	printf("배열 str의 크기: %d \n", sizeof(str)); //byte
	printf("널 문자 문자형 출력: %c \n", str[13]); //널 값
	printf("널 문자 정수형 출력: %d \n", str[13]); //널 값

	str[12] = '?'; //문자열 출력 = 변경
	printf("문자열 출력: %s \n", str);
	return 0;
}
```

이것을 보면 Null의 아스키 코드 값은 0, 문자는 미출력 된다는 사실을 알 수 있다.

공백문자의 아스키 코드 값은 32이 있기에 공백과 Null값은 다르다.



Scanf함수를 이용한 문자열을 입력했던 때가 있는데

그때 %d가 아닌 %s를 썼다. 그것이 str.



```c
int main(void)
{
	char str[50]; //배열
	int idx = 0; //변수 

	printf("문자열 입력: "); 
	scanf("%s", str); //문자열을 입력 받아 str에 저장
	printf("입력 받은 문자열: %s \n", str);  //배열은 &없음. 문자열만 

	printf("문자 단위 출력: ");
	while (str[idx] != '\0') //값이 Null이 아닐때까지 출력한다. - | /0 컷되는 컷반복문
	{
		printf("%c", str[idx]);
		idx++;
	}
	printf("\n");
	return 0;
}
```

배열 선언 후 변수를 입력했고 scanf를 통해서 문자열을 입력받는다. (문자와 문자열은 다르다..)

그 후 while반복문을 통해서 str배열을 출력해주는데 Null값이 아닐때 까지 출력이 된다.



이렇듯 이 케이스를 보면 Null문자가 중요하다는 사실을 알 수 있다.

Null이 있으면 문자열이고 Null이 없으면 문자열이 아닌 것이다.



```c
//Null이 필요한 경우

while (str[idx] != '\0')
{
	printf("%c", str[idx]);
	idx++;
}		
```

위 코드에서 이 부분만 똑 떼서 본다면? 

문자열에서 \0로 구분되는 것이 없다면 컴퓨터는 글의 끝을 알 수 없다.



```c
int main(void)
{
	char str[50] = "I like C programming";
	printf("string: %s \n", str);

	str[8] = '\0';     // 9번째 요소에 널 문자 저장
	printf("string: %s \n", str);

	str[6] = '\0';     // 7번째 요소에 널 문자 저장
	printf("string: %s \n", str);

	str[1] = '\0';     // 2번째 요소에 널 문자 저장
	printf("string: %s \n", str);
	return 0;
}
```

이 문구를 통해서 내가 입력한 문자열이 있는데 그 사이에 Null값을 넣어

출력을 바꿀 수 가 있다..! 즉 Null값은 문자의 종료다.



> 추가로 scnaf의 문자열의 입력특성이 있는데
>
> 우리가 He is my friend로 저장하면 He is my friend 4개로 저장된다.
>
> 즉 scanf는 문자열 입력으로 적합하지 않다..!



### 문제

```
문제1: 사용자로부터 하나의 영단어를 받아 입력받은 길이를 계산하는 프로그램을 출력하라.
```

```c
int main(void)
{
	char arr[50];
	int ea = 0;

	printf("영단어를 입력: ");
	scanf("%s", arr);

	while (arr[ea] != 0) //arr의 순차계산으로 0이 아닐때 반복
		ea++;

	printf("단어의 길이는 : %d입니다 \n", ea);
	return 0;
}
```

배열 크기는 적당히 지정하고 

아까 빈칸은 0으로 저장된다고 하였으니 0값이 아닐때까지 반복한 것에 대한 개수를 추출한다.

그러면 단어의 길이가 나온다.



```
문제2: 사용자로부터 영단어르 입력받아 char형에 저장. 그후 그 영단어를 역순으로 뒤집기
이때 널 위치 문자를 변경해서는 안되고 뒤집혔는지 체크
```

```c
int main(void)
{
	char arr[50];
	int ea = 0; //기입변수
	int i; //뒤집변수
	char temp; //잠깐 저장하는 변수

	printf("단어 입력: ");
	scanf("%s", arr);

	while (arr[ea] != 0) //값이 공백이 아닐때까지
		ea++;

	for (i = 0; i < ea / 2; i++) //조건은 ea/2로 한다 why? 반을 뒤집이면 어차피 반은 뒤집히니까
	{
		temp = arr[i]; //temp값에 임시저장
		arr[i] = arr[(ea - i) - 1]; //i번째 문자와 (ea-i)-1 번째 문자를 바꾼다.
		//ex) i=0 (ea-i)-1 = (5-0)-1 = 4 arr[0] 와 arr[4] 교환
		//ex) i=1 (ea-i)-1 = (5-1)-1 = 3 arr[1] 과 arr[3] 교환
		arr[(ea - i) - 1] = temp; // temp저장된 값을 arr의 [(ea - i) -1]에 넣기
	}
	printf("뒤집한 값 : %s \n", arr);
	return 0;
}
```

배열 지정 후 

기입을 변수와 뒤집을 변수, 그리고 임시저장 변수 3가지를 지정한다.



단어입력은 받은 후 그 값을 공백이 아닐때 까지 반복한다.

(공백이 되면 임시적으로 그 글자가 끝났다는 것)



반을 뒤집으면 나머지 반은 뒤집히니까 조건은 ea/2로 하고

temp를 통해 임시값 저장 그리고 문장을 뒤집는 것을 발생

그리고 그 값을 다시 임시값을 불러들여서

뒤집한 값을 출력한다.



```
문제3 : 사용자부터 영단어를 입력받는다. 그 후 영단어를 구성하는 문자중 아스키코드 값이 큰 것을 찾아 출력한다 
LOVE면 아스키 코드 값이 큰 V가 출력되어야한다.
```

```c
int main(void)
{
	char arr[50]; //배열
	int ea = 0; //길이 저장 변수
	int i; //인덱스
	char max = 0; //최대 아스키 코드 값 저장 변수

	printf("영단어 입력: ");
	scanf("%s", arr);

	while (arr[ea] != 0) //단어 길이 계산하기
		ea++;

	for (i = 0; i < ea; i++) // 0부터 시작해서 길이만큼
		if (max < arr[i]) //만약 max값보다 arr[i]이 크면
			max = arr[i]; //max값에 arr[i]을 넣어준다.
	// 0 <-> ?  이후 ?값이 크면 ?으로 그 이후 ? <-> n 비교 ?가 크면 ?를 넣어서
	// 큰값을 넣기.

	printf("가장 큰 아스키코드 값의 문자: %c \n", max);
	return 0;
}
```

배열을 지정해주고 길이 체크용 변수, 인덱스용 변수 

그리고 최대 아스키 코드값 저장 변수를 찾는다. (MAX값을 찾아야하니까)

그러면 while 반복문을 통해서 단어의 길이가 0이 아닐때까지 찾아서 길이를 계산하고

반복문 안에 if문을 달아서 더 큰값을 arr[i] 값에 넣어주어 최대값을 출력한다



이게 보니까 글을 너무 많이쓰면 난잡해져서 끊어쓰는 방식으로 여러번 올려야겠다.

다음은 포인터를 시작한다.
