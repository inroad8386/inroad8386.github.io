---
title: DataBase Duplication
date: 2024-02-04 00:10:01 
tags: 
description:
image: 
published: true
tags : ORACLE
---

## 데이터베이스 복사

서버DB의 데이터를 건드리면 위험하니까 일단 로컬DB로 복사하여 테스트 목적의 복사
<br>
현재 DB의 경우 과거에 받아두었던 최신화 되지 않은 DB가 있는 상태
<br>
<br>
<br>
<br>


## Toad for Orcale
![](/assets/img/20240204/frog.PNG)
<br><br>
DB 수정을 위해 Toad for Orcale 이라는 개구리를 사용
<br>
<br>
![](/assets/img/20240204/seci.PNG)
<br>
<br>
Database > SchemaBrowser 클릭 후 왼쪽 화면 탭에서 수정할 요소 선택
<br>
<br>
![](/assets/img/20240204/drop.PNG)
<br><br>
업데이트된 현재의 서버PC의 DB를 받아오기 위해 복사하는데 받아오면서 충돌나지 않게 하기 위해 본래 로컬DB에 있는 Table, Fuctions, Procedures 을 제거
<br>
<br><br><br><br>

## SQL Developer
**SQL Developer 열기**
<br> 먼저 SQL Developer를 엽니다.
<br>

**새 연결 설정**
<br>
복사할 데이터베이스에 대한 연결을 설정합니다. <br>
이를 위해 접속창에서 새로운 연결을 설정하고 관련 정보를 입력합니다. <br>
호스트, 포트, 사용자 이름 및 비밀번호와 같은 연결 정보를 입력합니다.<br>

![](/assets/img/20240204/db.PNG)
<br>
<br> SQL Developer 실행 > 도구 > 데이터베이스 복사



<br> <br> 
![](/assets/img/20240204/server1.PNG)
<br>
<br> 


**복사할 데이터베이스 선택**<br>
연결이 설정되면 연결된 데이터베이스를 선택합니다.<br>
"Connections" 창에서 데이터베이스를 우클릭하고 "Connect"를 선택하여 해당 데이터베이스에 연결합니다.<br>
<br>
<br>
 **소스접속** : Server DB접속<br> 
**대상접속** : 서버의 DB를 복사하여 붙여 넣을 DB를 선택<br> 

**소스와 대상을 헷갈리지 않도록 주의**
<br> 
<br> 



![](/assets/img/20240204/wifi.PNG)
<br><br> 
서버PC의 접속을 위해 네트워크를 연결한다.<br>
복사 전과 후 연결을 잘 체크하여 안전하게 실행할 것
<br><br>
<br>
![](/assets/img/20240204/select.PNG)<br>

**복사할 데이터베이스 개체 선택**<br>
복사하려는 테이블, 뷰 또는 다른 데이터베이스 개체를 선택합니다. 
<br>
선택한 데이터베이스 개체를 새로운 목적지 데이터베이스로 복사합니다. <br>
<br><br>


![](/assets/img/20240204/savedp.PNG)
<br><br>
데이터베이스 복사 완료
<br><br><br>

**복사 확인**<br>
데이터베이스 개체가 성공적으로 복사되었는지 확인합니다.<br>
필요에 따라 대상 데이터베이스를 새로 고쳐 새로운 데이터베이스 개체를 확인할 수 있습니다.<br><br>

