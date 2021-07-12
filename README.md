
# vapor와 heroku를 이용한 API 서버 구현



## 📌 학습 키워드

* REST를 고려한 API 설계
* Request/Response body의 각각 키에 해당하는 데이터 타입 정의
* HTTP 상태 코드 및 메세지 활용
* Heroku 배포
* Fluent ORM을 활용하여 SQL 입력 없이 DB 테이블 생성
* Model과 DTO(Data Transfer Object)의 정의와 활용
* EventLoopFuture 타입의 이해와 활용
* AbortError 타입의 정의와 

##📌 Commit Convention 

Type|Emoji|Description
:---|:---:|:---
Feat      |✨| 기능 (새로운 기능)
Fix       |🐛| 버그 (버그 수정)
Refactor	|♻️| 리팩토링
Style	    |💄| 스타일 (코드 형식, 세미콜론 추가: 비즈니스 로직에 변경 없음)
Docs	    |📝| 문서 (문서 추가, 수정, 삭제)
Test	    |✅| 테스트 (테스트 코드 추가, 수정, 삭제: 비즈니스 로직에 변경 없음)
Chore	    |🔧| 기타 변경사항 (빌드 스크립트 수정 등)
Comment	  |💡| 필요한 주석 추가 및 변경
Rename    |🚚| 파일 혹은 폴더명을 수정하거나 옮기는 작업만인 경우
Remove    |🔥| 파일을 삭제하는 작업만 수행한 경우


```
ex) 

✨ [Feat] : Vapor App 베포함
```

<br>

## 📌 Pull Request

* [Step 1](https://github.com/yagom-academy/ios-project-manager-server/pull/20)
* [Step 2](https://github.com/yagom-academy/ios-project-manager-server/pull/24)
* [Step 3](https://github.com/yagom-academy/ios-project-manager-server/pull/29)

<br>

## 📌 API 문서

[작성한 API 문서](https://docs.google.com/spreadsheets/d/1PTOGFh9kAbBUtQZ0pqC8j2-oCjURtjUnjwxA2t6TlAU/edit#gid=0)

[API 문서 다운로드](https://github.com/alwaysblu/ios-project-manager-server/blob/main/API_Document.pdf)

<br>

## 📌 구현 사항

### 실행

#### 실패 조건

- `UUID` : 36 자릿수 제한, 데이터베이스에 존재하는 ID
- `Title` : 공백 *(ex : "title" : "" )*
- `Description` : 1000자 초과
- `Date` : 10 자릿수 (100억초 미만)
- `Status` : ["todo", "doing", "done"] 포함되지 않는 경우
- `Content Type` : aplication/json 타입이 아닌 경우



### POST

#### 성공

<img width="1066" alt="스크린샷 2021-07-06 오전 11 33 31" src="https://user-images.githubusercontent.com/75533266/125306786-755d0100-e36a-11eb-866f-910bcf4d8b12.png">


#### 실패

- 파라미터 오류

<img width="1400" alt="스크린샷 2021-07-06 오전 11 34 25" src="https://user-images.githubusercontent.com/75533266/125306846-83128680-e36a-11eb-85e2-e6d1b82cf81c.png">


- Content Type 오류 (aplication/json)

<img width="1383" alt="스크린샷 2021-07-06 오전 11 38 16" src="https://user-images.githubusercontent.com/75533266/125306859-86a60d80-e36a-11eb-99fa-dc3cce3c1688.png">


- Status 파라미터 오류

<img width="1384" alt="스크린샷 2021-07-06 오전 11 39 13" src="https://user-images.githubusercontent.com/75533266/125306875-8a399480-e36a-11eb-93c6-392e0b3fc7c9.png">


#### 확인 (GET)

<img width="1403" alt="스크린샷 2021-07-06 오전 11 35 15" src="https://user-images.githubusercontent.com/75533266/125306888-8d348500-e36a-11eb-87c6-c041bcd9b23a.png">


------

### PATCH

#### 성공

<img width="1401" alt="스크린샷 2021-07-06 오전 11 36 27" src="https://user-images.githubusercontent.com/75533266/125306904-8f96df00-e36a-11eb-9956-bbf37a27859c.png">


#### 실패

- 파라미터

<img width="1384" alt="스크린샷 2021-07-06 오전 11 37 28" src="https://user-images.githubusercontent.com/75533266/125306917-932a6600-e36a-11eb-9dab-aaba8ab912cd.png">


- 잘못된 ID 전달

<img width="1386" alt="스크린샷 2021-07-06 오후 12 01 47" src="https://user-images.githubusercontent.com/75533266/125306926-958cc000-e36a-11eb-93d9-31c917fe72eb.png">


- 잘못된 ID 형식 (UUID)

<img width="1388" alt="스크린샷 2021-07-06 오후 12 03 07" src="https://user-images.githubusercontent.com/75533266/125306933-97ef1a00-e36a-11eb-996b-5253c499915d.png">


- Content Type 오류

<img width="910" alt="스크린샷 2021-07-06 오후 4 09 29" src="https://user-images.githubusercontent.com/75533266/125306955-9aea0a80-e36a-11eb-8549-65d64b50a694.png">


#### 확인 (GET)

- 좌 (PATCH) - 수정

<left><img src="https://user-images.githubusercontent.com/75533266/125306982-a0475500-e36a-11eb-92c7-03c32ae495b4.png" width="35%"><left><img src="https://user-images.githubusercontent.com/75533266/125307015-a6d5cc80-e36a-11eb-96f8-c9939b40a4d5.png" alt="image-20210706155718973" width="55%">
  

  
  

------

### DELETE

#### 성공

  <img width="1387" alt="스크린샷 2021-07-06 오전 11 46 08" src="https://user-images.githubusercontent.com/75533266/125307541-1946ac80-e36b-11eb-946d-cd4595336b8c.png">


#### 실패

- 데이터베이스에 없는 ID 입력

  <img width="913" alt="스크린샷 2021-07-06 오후 4 08 57" src="https://user-images.githubusercontent.com/75533266/125307554-1d72ca00-e36b-11eb-84ab-d52a85c4bf35.png">


#### 확인 (GET)

  <img width="1385" alt="스크린샷 2021-07-06 오전 11 46 23" src="https://user-images.githubusercontent.com/75533266/125307563-1fd52400-e36b-11eb-8aab-6a401703f9cc.png">


