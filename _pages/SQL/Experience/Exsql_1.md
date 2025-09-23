---
title: "데이터 시각화 SQL #1"
date: "2025-09-23"
thumbnail: "/assets/img/thumbnail/postsql.jpg"
---

## 개요

해당 강의는 블로그에 올리면 안되서 유출이 되지 않는 선에서 대충 깨달은 내용만 정리하고자 한다.

SQL을 통해서 시각화를 구축하는 것 큰 목적은 그것이고

PostgreSQL , DBeaver 을 사용한다.



1.SQL Alchemy에서 PostgreSQL에 Connection연결

2.Pandas는 SQLAlchemy로 만든 DB Con이용하여 SQL호출 후 결과를 DF에 저장

3.Plotly(python기반 시각화)는 DF와 연동하여 시각화를 수행한다.



이때 왜 Pandas를 연계하는가? 

Plotly가 Pandas(DF)와 연계되기 쉬움 (X축과 Y축을 구현해서 쉽게 시각화를 만들 수 있음.)

우리의 Data는 PostgreSQL에 있음. 이때 Pandas의 데이터 넣는 작업은 SQLAlchemy가 해준다.



해당 강의는 여러가지 차트가 있지만 

1. 바차트 - 특정컬럼 이산 값(X축)에 따른 다른 컬럼의 연속형 값을 시각화
2. 라인차트 - 시계열 데이터(Tiem Data)를 시각화 하며 X축 일자, Y축에 연속형 값으로 시각화
3. 바 차트에 + 라인차트 섞기
4. 트리맵과 퍼널차트

정도 하는 것 같다.



## 분석 조건

일단 ERD를 이해하는 것이 중요하다.

각 테이블 별로 연결되는 관계차수와 PK, FK등에 대한 부분을 체크한다.



