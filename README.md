## iOS 커리어 스타터 캠프

### 프로젝트 관리 앱 서버 프로젝트 저장소



### < Commit Convention >

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

![스크린샷 2021-07-06 오전 11.33.31](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.33.31.png)

#### 실패

- 파라미터 오류

![스크린샷 2021-07-06 오전 11.34.25](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.34.25.png)

- Content Type 오류 (aplication/json)

![스크린샷 2021-07-06 오전 11.38.16](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.38.16.png)

- Status 파라미터 오류

![스크린샷 2021-07-06 오전 11.39.13](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.39.13.png)

#### 확인 (GET)

![스크린샷 2021-07-06 오전 11.35.15](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.35.15.png)

------

### PATCH

#### 성공

![스크린샷 2021-07-06 오전 11.36.27](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.36.27.png)

#### 실패

- 파라미터

![스크린샷 2021-07-06 오전 11.37.28](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.37.28.png)

- 잘못된 ID 전달

![스크린샷 2021-07-06 오후 12.01.47](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오후 12.01.47.png)

- 잘못된 ID 형식 (UUID)

![스크린샷 2021-07-06 오후 12.03.07](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오후 12.03.07.png)

- Content Type 오류

![스크린샷 2021-07-06 오후 4.09.29](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오후 4.09.29.png)

#### 확인 (GET)

- 좌 (PATCH) - 수정

<left><img src="/Users/choejeongmin/Downloads/image-20210706155611151.png" alt="image-20210706155611151" style="zoom:40%;" /><left><img src="/Users/choejeongmin/Downloads/image-20210706155718973.png" alt="image-20210706155718973" style="zoom:41%;" />

------

### DELETE

#### 성공

![스크린샷 2021-07-06 오전 11.46.08](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.46.08.png)

#### 실패

- 데이터베이스에 없는 ID 입력

![스크린샷 2021-07-06 오후 4.08.57](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오후 4.08.57.png)

#### 확인 (GET)

![스크린샷 2021-07-06 오전 11.46.23](/Users/choejeongmin/Downloads/스크린샷 2021-07-06 오전 11.46.23.png)

