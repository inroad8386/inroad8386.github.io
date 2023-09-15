---
title: MX Component - PLC 통신
date: 2023-09-14 09:58:47 
tags: 
description:
image: 
published: true
tags : study
---

## MX component
프로토콜을 의식하지 않고도 PC에서 PLC나 모션 컨트롤러로의 통신을 <br>간단히 처리할 수 있는 Active X® 컨트롤, .NET 컨트롤 라이브러리
<br>
<br>
번거롭고 복잡했던 시리얼 통신이나 Ethernet 통신을 실행하는<br> 애플리케이션의 개발이 MX Component를 사용함으로써 매우 간단해짐
<br>

## GX Works 2 / Gx Works 3 차이
대응 하는 PLC 가 다름<br>
Works2 : QCPU, LCPU, FXCPU 등 이하 CPU <br>
Works3 : 최신 RCPU, FX5CPU, NCCPU 등 <br>

## Word (워드)
워드 데이터는 16개의 bit, 2개의 byte 수치 데이터를 말함<br>
표기 방법은 10진수와 16진수로 할 수 있음<br>
65,536가지 수를 표현할 수 있으며 10진수로 표현 시 0~65,535까지 가능<br>



## 설치 프로그램

1)  Communication Setup utility<br>
2)  GX Works 2 <br>
3)  PLC Monitor Utility<br>

⚠️ 설치 후 실행시 관리자 권한 으로 실행할 것 <br>



## Step1 

1.   Communication Setup Utility 관리자 권한으로 실행<br>
2.   Wizard 클릭<br>
3.   Logical Station number 0 입력<br>
4.   Comment 이름설정<br>

## Step2
1.  GX Works 2 관리자 권한으로 실행<br>
2. New Project 생성 후 Ladder 작성<br><br>
![test](https://github.com/inroad8386/inroad8386.github.io/blob/main/assets/img/PLC.PNG?raw=true)
[설정]<br>
Project Type : Simple Project<br>
PLC Series : QCPU (Q mode)<br>
PLC Type : Q02/Q02H<br>
Language : Ladder<br>

[단축키]<br>
Shift + Insert : 줄 추가<br>
Shift + Delete : 줄 삭제<br>
접점 단축키 : F5<br>

Shift +insert 로 줄 추가<br>
F5 누르고 접점에 M0 입력<br>
F7 누르고 RND D0 입력<br>
F4 눌러서 출력<br>






