---
title: "엑셀 대시보드 제작"
date: "2025-02-16"
thumbnail: "/assets/img/thumbnail/Excel.jpg"
---

## 엑셀 대시보드 제작

엑셀에서 데이터가 주어지면 그것을 가공하는 느낌으로

오랜만에 데이터를 정규화 시킨 후 그것을 피벗테이블로 가공하고

마지막으로 슬라이서를 이용해서 만드는 대시보드를 연습해보려고 한다.



쉽게 총 3단계로 이루어진다.



>    1.데이터들이 입력된다.
>
> 2. 데이터를 기반으로 피벗테이블을 제작한다.
> 3. 피벗테이블을 기반으로 슬라이서를 제작한다.



이렇게 하여 대시보드에서 데이터를 누적하는 순간 변동하는 것이다.



실제 외주를 받거나 업무에서 사용하는 재료들은 사용할 수 없으니

그냥 게임용 취미로 만든 대시보드로 적으려고 한다.



## 내용

![체크](../../../images/dashboard/체크.png)

해당 내용은 하는 게임 중 하나인 로스트아크를 기반으로 만들었으며,



순서로는 크게

데이터를 제작한다.

데이터를 분류 시킬 정보를 추가 시킨다. 

그리고 피벗테이블을 추가한 후 슬라이서를 늘린다.



최종적으로는 내가 보고 싶은 데이터가 무엇인가를 구현하는 것이 필요하다.

1. 캐릭터별로 어떤 레이드에서 얼마만큼의 재화를 생산하는가?
2. 캐릭터별로 생산재화 - 소비재화를 합했을 때 어느정도인가?
3. 캐릭터 강화 외, 추가적인 재화
4. 캐릭터 강화 외, 재료 준비 등의  재화



피벗테이블로 해당 4개의 내용을 구축시킨 후,

슬라이서를 통해서 누르면 변동되게끔 바꾼다.



여기서 주의할 점은 표의 내용이 늘어나면 자동으로 피벗에 적용되도록 하는 것이다.



캐릭터별로 표로 보는 방법이 있지만,

결국에 칸이 너무 많이 차지하고 한장으로 보이기 쉽지 않다는 단점이 있다.



대시보드를 통해서 기간별정보, 분류별 정보를 선택하여 볼 수 있고,

해당 내용과 연결하여 월별지출, 총지출을 계산할 수 있다.



이를 통해서 데이터  수집 => 데이터 정규화 => 분류 생각 => 피벗 => 대시보드 제작이다.



아마 최근 SQL <-> Excel을 배우고 있는데 이를 통한다면 좀 더 방대한 자료를 넣어도

부담이 없을지도?



그래도 SQL를 쓰는 기업보다 Excel쓰는 기업이 많으니 둘다 알아두는거로 하자.!



>알아두기.
>
>1.데이터정규화
>
>2.데이터피벗
>
>3.데이터슬라이서
>
>4.추가적으로 함수정도?





아마 추가적인 지식이 있으면 여기에 실험 후 올리러 올 예정이다.
