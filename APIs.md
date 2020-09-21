# APIs

에너지 지킴이 프로젝트의 API 명세 및 Description

## APIs 목차

-   [공통](#공통)
-   [API Response 구조](#api-response-구조)
-   [Device API](#device-api)
-   [Device Control API](#device-control-api)
-   [RaspberryPi API](#raspberrypi-api)
-   [Web API](#web-api)

## 공통

-   모든 API request, response의 `Content-Type`은 `application/json`이다.

## API Response 구조

-   message(String) : 에러메시지
-   data : 해당 API의 response body

예시)

```json
{
    "message": "",
    "data": {
    }
}
```

## Device API

- `GET /api/device` - 디바이스 등록 정보 조회 API

  - description : 등록된 디바이스에 대한 정보를 가져옵니다.

  - method : GET

  - URI : /api/device

  -   request header :
      
      -   `Content-Type` : `application/json`
      -   `Authentication`:`Bearer <token>`
  
- param:  device_id(String) : 디바이스의 식별 아이디
  
- request body:

  -   response header:
      
      -   `Content-Type` : `application/json`
      
  - response body:

    -   device_type(String) : 디바이스의 유형
    -   device_ip(String) : 디바이스 IP Address
    -   unit_count(Integer) : ON/OFF 가능한 장치의 개수
    -   units(Array) :
        -   index(Integer) : 디바이스에 연결된 유닛들의 인덱스 
        -   on_off(Boolean) : 디바이스에 연결된 유닛들의 ON/OFF 상태

    }

  - error response:
    - 404 (Page Not Found)

      -   message : "해당 디바이스 정보를 찾을 수 없습니다."
      -   data: {}
    - 401  (Unauthorized)

      -   message : "접근 권한이 없습니다."

      -   data: {}

- `POST /api/device` - 디바이스 등록 API

  - description : 새로운 디바이스에 대한 정보를 등록합니다.
  - method : POST
  - URI : /api/device
  -   request header :
      
      -   `Content-Type` : `application/json`
      -   `Authentication`:`Bearer <token>`
  - param : X
  - request body:

    -   device_id(String) : 디바이스 식별 아이디
    -   device_type(String) : 디바이스의 유형(스위치 or 플러그 or ETC …)
    -   device_ip(String) : 디바이스 IP Address
    -   unit_count(Integer) : ON/OFF 가능한 장치의 개수(스위치라고 하면 서보모터의 개수, 플러그이면 SSR의 개수)
  - response header: X
  - response body: 

    - 200
      - message : "디바이스 정보가 등록되었습니다."
      - data:{}
  - error response body:
    - 401 (Unauthorized)
      - message: "접근 권한이 없습니다."
      - data:{}

- `PUT /api/device` - 디바이스 등록 정보 수정 API

  -   description : 등록된 디바이스 정보를 수정합니다.
  -   method : PUT
  -   URI : /api/device
  -   request header :
      -   `Content-Type` : `application/json`
      -   `Authentication`:`Bearer <token>`
  -   param: X
  -   request body:
      -   device_id(String) : 수정할 디바이스의 식별 아이디
      -   device_type(String) : 디바이스의 유형을 이 값으로 수정
      -   device_ip(String) : 디바이스 IP Address
      -   unit_count(int) : ON/OFF 가능한 장치의 개수를 이 값으로 수정
  -   response header: x
  -   response body: 
      -   200
          -   message : "디바이스 정보가 수정되었습니다."
          -   data :{} 
  -   error response body:
      -   404 (Page Not Found)
          -   message : "수정할 디바이스 정보를 찾을 수 없습니다,"
          -   data:{}
- `DELETE /api/device` - 디바이스 등록 정보 삭제 API

  -   description : 등록된 디바이스 정보를 삭제합니다.
  -   method : DELETE
  -   URI : /api/device
  -   request header :
      -   `Content-Type` : `application/json`
      -   `Authentication`:`Bearer <token>`
  -   param: X
  -   request body:
      
      -   device_id(String) : 삭제할 디바이스의 식별 아이디
  -   response header: X
  -   response body: 
      -   200
          -   message: "디바이스 정보가 삭제되었습니다."
          -   data :{}
  -   error response body:
      -   401 (Unauthorized)
          -   message: "접근 권한이 없습니다."
          -   data:{}
      -   404 (Page Not Found)
          -   message:"삭제할 디바이스 정보를 찾을 수 없습니다."
          -   data:{}
          
          

## RaspberryPi API

- `POST /api/raspberry/connect` - 라즈베리파이 연결 API
  -   description : 라즈베리파이와 연결합니다.
  -   method : POST
  -   URI : /api/raspberry/connect
  -   request header :
      
      -   `Content-Type`:`application/json`
  -   param : X
  -   request body:
      -   raspberry_id(String) : 조회할 라즈베리파이 식별 아이디
      -   raspberry_pw(String) : 조회할 라즈베리파이 비밀번호
  -   response header :
      
      -   `Content-Type` : `application/json`
  -   response body :
      
      -   access_token :  ''"
      -   refresh_token : ""
  - error response body:
    - 400 (Bad Request)
-   message : "아이디 혹은 패스워드가 일치하지 않습니다."
      -   data:{}
    




-   `GET /api/raspberry` - 라즈베리파이 등록 정보 조회 API
- description : 라즈베리파이 등록 정보를 가져옵니다.
  -   method : GET
  -   URI : /api/raspberry
  -   request header : 
      
      -   `Authentication`:`Bearer <token>`
  -   param : X
  -   request body: X
  -   response header :
      
      -   `Content-Type` : `application/json`
  -   response body:
      -   raspberry_group(String) : 조회할 그룹
      -   raspberry_id(String) : 라즈베리파이 식별 아이디
      -   remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능. 만약 False 시 raspberry_devices는 빈 배열.
      -   raspberry_devices(Array) :[
          -   device_id : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
          -   device_type(String) : 조회한 라즈베리파이에 연결된 디바이스 유형
          
          ]
  -   error response body:
-   `POST /api/raspberry` - 라즈베리파이 등록 API

    -   description : 새로운 라즈베리파이 정보를 등록합니다.
    -   method: POST - URI : /api/raspberry
    -   request header :
        -   `Content-Type` : `application/json`
            -   param: X
            -   request body
                -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디(ex DSM_blabla)
                -   raspberry_id(String) : 라즈베리파이 식별 아이디(디바이스 연결 시 사용)
                -   raspberry_pw(String) : 라즈베리파이 비밀번호(디바이스 연결 시 사용)
                -   remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능.
    -   response header: X
    -   response body: 
        -   201 (Created)
            -   "message": "라즈베리파이 정보가 등록되었습니다."
    -   error response body:
-   `PUT /api/raspberry` - 라즈베리파이 등록 정보 수정 API
    -   description : 등록된 라즈베리파이 정보를 수정합니다.
    -   method: POST - URI : /api/raspberry
    -   request header :
        -   `Content-Type` : `application/json`
    -   param: X
    -   request body
        -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
        -   raspberry_id(String) : 라즈베리파이 식별 아이디(디바이스 연결 시 사용)
        -   raspberry_pw(String) : 수정할 라즈베리파이 비밀번호(디바이스 연결 시 사용)
        -   remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능.
        -   raspberry_devices(Array) :
            -   device_id(String) : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
            -   device_type(String) : 조회한 라즈베리파이에 연결된 디바이스 유형
    -   response header: X
    -   response body: X
    -   error response body:
- `DELETE /api/raspberry` - 라즈베리파이 등록 정보 삭제 API
  -   description : 등록된 라즈베리파이 정보를 삭제합니다.
  -   method : DELETE
  -   URI : /api/raspberry
  -   request header :`Authentication`:`Bearer <token>`
  -   param: X
  -   request body:
  -   response header: X
  -   response body: X
  -   error response body:
      -   404 (Not Found)
          -   message : "삭제할 라즈베리파이 정보가 없습니다."
          -   data : {}
      -   401  (Unauthorized)
          -   message: "접근 권한이 없습니다."
          -   data:{}



## Web API

- `POST /api/web/login` - 로그인

  - description : 등록된 라즈베리파이 로그인.

  - method : POST

  - URI : /api/web/login

  - request header :`content-type`:`application/json`

  - param: X

  - request body:

    - raspberry_group : 라즈베리파이 그룹
    - raspberry_id : 라즈베리파이 아이디
    - raspberry_pw : 라즈베리파이 패스워드

  - response header: 

  - response body: 

    - 200:
      - access_token : 
      - refresh_token:

  - error response body:

    - 400 (Bad Request)

      -   message : "아이디 혹은 패스워드가 일치하지 않습니다."
      -   data:{}

      

- `GET api/web/devices`

  - description : 디바이스들의 정보를 가져온다.

  - method : GET

  - URI : /api/web/devices

  - request header :

    - `authorization`: `Bearer <token>`

  - param: X

  - request body: X

  - response header: 

  - response body: 

    - 200:

      - devices:[

        - {
        - "device_id" : "dsm11_1" - 디바이스 아이디
        - "device_type" : "switch", - 디바이스 타입
        - "unit_count" : 3   - 디바이스마다 유닛들 갯수
        - }

        ]

  - error response body:

    - 401 (Unauthorized)

      -   message : "접근 권한이 없습니다."
      -   data:{}

      

- `GET api/web/units`

  - description : 유닛들의 정보를 가져온다. 디바이스들의 정보에서 가져온 유닛들의 갯수를 받고 인덱스로 접근하면 된다.

  - method : GET

  - URI : /api/web/units

  - request header :

    - `content-type`:`application/json`
    - `authorization`: `Bearer <token>`

  - param: "device_id" : "dsm11_1" - 유닛들이 속한 디바이스의 아이디

  - request body: X

  - response header: 

  - response body: 

    - 200:

      - units : [

        - "index" : 0 - 유닛 인덱스
        - "on_off" : true - 유닛이 켜져있는지 꺼져있는지

        ]

  - error response body:

    - 401 (Unauthorized)
      -   message : "아이디 혹은 패스워드가 일치하지 않습니다."
      -   data:{}

  

-   `GET /api/web/using-time` - 사용시간 조회 API
    -   description : 라즈베리파이의 전력 사용시간을 조회합니다.
    -   method: GET
    -   URI: /api/web/using-time
    -   request header: X
    -   param:
        -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
        -   raspberry_id(String) : 라즈베리파이 식별 아이디, 빈 문자열일 경우 그룹 내 전체 라즈베리파이를 대상으로 조회
        -   sort(Boolean) : usage_time을 기준으로 true시 오름차순 정렬. false시 내림차순 정렬.
        -   year(Boolean) : 최근 year_n년동안의 전력 사용시간 조회. False 시 조회하지 않음
        -   year_n(Integer) : 최근 몇 년을 조회할 것인지 결정. year가 False일 경우 의미 없음.
        -   month(Boolean) : 최근 month_n달동안의 전력 사용시간 조회. False 시 조회하지 않음.
        -   month_n(Integer) : 최근 몇 달을 조회할 것인지 결정. month가 False일 경우 의미없음.
        -   week(Boolean) : 최근 week_n주동안의 전력 사용시간 조회. False 시 조회하지 않음
        -   week_n(Integer) : 최근 몇 주를 조회할 것인지 결정. week가 False일 경우 의미없음.
        -   day(Boolean) : 최근 day_n일 동안의 전력 사용시간 조회. False 시 조회하지 않음.
        -   day_n(Integer) : 최근 며칠을 조회할 것인지 결정. day가 False일 경우 의미없음.
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   usage_times:
            -   year(Array): 최근 year_n년 동안의 전력 사용시간. year가 false일경우 빈 배열.
                -   raspberry_id(String) : 라즈베리파이 아이디
                -   usage_time(Double) : 사용 시간(단위: 시간. 소수점 아래 : 분)
            -   month(Array): 최근 month_n달 동안의 전력 사용시간. month가 false일경우 빈 배열.
                -   raspberry_id(String) : 라즈베리파이 아이디
                -   usage_time(Double) : 사용 시간(단위: 시간. 소수점 아래 : 분)
            -   week(Array): 최근 week_n주 동안의 전력 사용시간.week가 false일경우 빈 배열.
                -   raspberry_id(String) : 라즈베리파이 아이디
                -   usage_time(Double) : 사용 시간(단위: 시간. 소수점 아래 : 분)
            -   day(Array): 최근 day_n일 동안의 전력 사용시간.day가 false일경우 빈 배열.
                -   raspberry_id(String) : 라즈베리파이 아이디
                -   usage_time(Double) : 사용 시간(단위: 시간. 소수점 아래 : 분)
    -   error response body:



