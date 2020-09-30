# APIs

에너지 지킴이 프로젝트의 API 명세 및 Description

## APIs 목차

-   [공통](#공통)
-   [API Response 구조](#api-response-구조)
-   [Device API](#device-api)
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
    "data": ""
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
  
- param:  

  - device_id(String) : 디바이스의 식별 아이디
  - device_type(String) : 디바이스의 유형

- request body:X

- response header:

- response body:

  -   device_ip(String) : 디바이스 IP Address
  -   unit_count(Integer) : ON/OFF 가능한 장치의 개수
  -   units(Array) :
      -   index(Integer) : 디바이스에 연결된 유닛들의 인덱스 
      -   on_off(Boolean) : 디바이스에 연결된 유닛들의 ON/OFF 상태

  }

  - error response:
    - 404 (Page Not Found)

      -   message : "해당 디바이스 정보를 찾을 수 없습니다."
    - 401  (Unauthorized)
    
    - message : "접근 권한이 없습니다."
    
      



- `POST /api/device` - 디바이스 등록 API

  - description : 새로운 디바이스에 대한 정보를 등록합니다.
  - method : POST
  - URI : /api/device
  -   request header :
      
      -   `Content-Type` : `application/json`
  - param : X
  - request body:

    -   device_id(String) : 디바이스 식별 아이디
    -   device_type(String) : 디바이스의 유형(스위치 or 플러그 or ETC …)
    -   unit_count(Integer) : ON/OFF 가능한 장치의 개수(스위치라고 하면 서보모터의 개수, 플러그이면 SSR의 개수)
    -   device_ip(String) : 디바이스 IP Address
  - response header: X
  - response body: 

    - 200
      - message : "디바이스 정보가 등록되었습니다."
      
    
  - error response body:
    - 401 (Unauthorized)
      
      - message: "접근 권한이 없습니다."
      
        
      
      

- `PUT /api/device` - 디바이스 등록 정보 수정 API

  -   description : 등록된 디바이스 정보를 수정합니다.
  -   method : PUT
  -   URI : /api/device
  -   request header :
      -   `Content-Type` : `application/json`
  -   param: X
  -   request body:
      -   device_id(String) : 수정할 디바이스의 식별 아이디
      -   device_type(String) : 디바이스의 유형을 이 값으로 수정
      -   device_ip(String) : 디바이스 IP Address
  -   response header: x
  
  -   response body: 
      -   200
          
          - message : "디바이스 정보가 수정되었습니다."
          
      
  -   error response body:
      -   404 (Page Not Found)
          - message : "수정할 디바이스 정보를 찾을 수 없습니다,"
          
  
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
      -   device_type(String) : 삭제할 디바이스의 타입
  -   response header: X
  -   response body: 
      -   200
          
          - message: "디바이스 정보가 삭제되었습니다."
          
      
  -   error response body:
      -   401 (Unauthorized)
          
          - message: "접근 권한이 없습니다."
          
            
          
      -   404 (Page Not Found)
          -   message:"삭제할 디바이스 정보를 찾을 수 없습니다."
          
          

- `POST /api/device/control` - 디바이스 컨트롤 API

  - description : 디바이스에 연결된 유닛들을 컨트롤 합니다.

  - method : POST

  - URI : /api/device

  - request header :

    -   `Content-Type` : `application/json`
    -   `Authentication`:`Bearer <token>`

  - param: X

  - request body:

    -   device_id(String) : 삭제할 디바이스의 식별 아이디
    -   device_type(String) : 삭제할 디바이스의 타입
    -   on_off(Boolean) : 유닛의 킬지 말지 정한다.
    -   unit_index(Integer) : 유닛의 인덱스

  - response header: X

  - response body: 

    - 200

      - message: "디바이스를 성공적으로 제어했습니다."

        

  - error response body:

    - 401 (Unauthorized)

      - message: "접근 권한이 없습니다."

        

    - 404 (Page Not Found)

      -   message:"컨트롤할 디바이스 정보를 찾을 수 없습니다."

## RaspberryPi API

- `POST /api/raspberry/connect` - 라즈베리파이 연결 API
  - description : 라즈베리파이와 연결합니다.

  - method : POST

  - URI : /api/raspberry/connect

  -   request header :
      
      -   `Content-Type`:`application/json`
      
  - param : X

  -   request body:
      -   raspberry_group(String) : 조회할 라즈베리파이 그룹
      -   raspberry_id(String) : 조회할 라즈베리파이 식별 아이디
      -   raspberry_pw(String) : 조회할 라즈베리파이 비밀번호
      
  -   response header :
      
      -   `Content-Type` : `application/json`
      
  -   response body :
      
      -   200
          -   access_token :  ''"
      
  - error response body:
    
    - 400 (Bad Request)
      - message : "아이디 혹은 패스워드가 일치하지 않습니다."
    
    


- `GET /api/raspberry` - 라즈베리파이 등록 정보 조회 API


  - description : 라즈베리파이 등록 정보를 가져옵니다.
    
  - method : GET

  - URI : /api/raspberry

  - request header : 

    -   `Content-Type`:`application/json`
    -   `Authentication`:`Bearer <token>`

  - param : X

  - request body: 

  - response header :

    -   `Content-Type` : `application/json`

  - response body:
    - remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능. 만약 False 시 raspberry_devices는 빈 배열.

    - devices(Array) :

      -   device_id(String) : 조회할 라즈베리파이에 연결된 디바이스 아이디
      -   device_ip(String) : 조회할 라즈베리파이에 연결된 디바이스 아이피

      ]

  - error response body:

  

- `POST /api/raspberry` - 라즈베리파이 등록 API

  - description : 새로운 라즈베리파이 정보를 등록합니다.

  - method: POST - URI : /api/raspberry

  - request header :
    - `Content-Type` : `application/json`

      -   param: X
      - request body
        - raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디(ex DSM_blabla)

        - raspberry_id(String) : 라즈베리파이 식별 아이디(디바이스 연결 시 사용)

        - raspberry_pw(String) : 라즈베리파이 비밀번호(디바이스 연결 시 사용)

        - remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능.

        - devices(Array) : [{

          - device_id(String) : 디바이스 아이디

          - device_type(String) : 디바이스 아이피

            }]

  - response header: X

  -   response body: 
      -   201 (Created)
          -   "message": "라즈베리파이 정보가 등록되었습니다."
      
  -   error response body:

  

- `PUT /api/raspberry` - 라즈베리파이 등록 정보 수정 API

  -   description : 등록된 라즈베리파이 정보를 수정합니다.
  -   method: POST - URI : /api/raspberry
  -   request header :
      -   `Content-Type` : `application/json`
      -   `Authentication`:`Bearer <token>`
  -   param: X
  -   request body
      -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
      -   raspberry_id(String) : 라즈베리파이 식별 아이디(디바이스 연결 시 사용)
      -   raspberry_pw(String) : 수정할 라즈베리파이 비밀번호(디바이스 연결 시 사용)
      -   remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능.
  -   response header: X
  -   response body: X
  -   error response body:
- `DELETE /api/raspberry` - 라즈베리파이 등록 정보 삭제 API
  
  - description : 등록된 라즈베리파이 정보를 삭제합니다.
  
  - method : DELETE
  
  - URI : /api/raspberry
  
  - request header :
  
    -   `Authentication`:`Bearer <token>`
  
  - param: X
  
  - request body:
  
  - response header: X
  
  - response body: X
  
  -   error response body:
      -   404 (Not Found)
          
          -   message : "삭제할 라즈베리파이 정보가 없습니다."
      -   401  (Unauthorized)
          
          - message: "접근 권한이 없습니다."
          
            



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
  
- error response body:
  
  - 400 (Bad Request)
  
    - message : "아이디 혹은 패스워드가 일치하지 않습니다."
      
    
    
    

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
        - "unit_info" : [false, true, false]   - 디바이스의 유닛들마다 on/off상태
  - }
        
      ]
  
- error response body:
  
  - 401 (Unauthorized)
  - message : "접근 권한이 없습니다."
    
  



- `GET /api/web/using-time` - 사용시간 조회 API

  -   description : 라즈베리파이의 전력 사용시간을 조회합니다.
  -   method: GET
  -   URI: /api/web/using-time
  -   request header: X
  -   param:
      -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
      -   raspberry_id(String) : 라즈베리파이 식별 아이디, 빈 문자열일 경우 그룹 내 전체 라즈베리파이를 대상으로 조회
      -   year(Boolean) : 최근 year_n년동안의 전력 사용시간 조회. False 시 조회하지 않음
      -   year_n(Integer) : 최근 몇 년을 조회할 것인지 결정. year가 False일 경우 의미 없음.
      -   month(Boolean) : 최근 month_n달동안의 전력 사용시간 조회. False 시 조회하지 않음.
      -   month_n(Integer) : 최근 몇 달을 조회할 것인지 결정. month가 False일 경우 의미없음.
      -   day(Boolean) : 최근 day_n일 동안의 전력 사용시간 조회. False 시 조회하지 않음.
      -   day_n(Integer) : 최근 며칠을 조회할 것인지 결정. day가 False일 경우 의미없음.
  -   request body: X
  -   response header:
      
      -   `Content-Type` : `application/json`
  - response body:
    - usage_times:
      -   year(Array): 최근 year_n년 동안의 전력 사용시간. year가 false일경우 빈 배열.[[
          -   <년도>(String) : ex) '2015', '2016', '2017' 
          -   usage_time(int) : 사용 시간(단위 : 초)
          
          ]]

      -   month(Array): 최근 month_n달 동안의 전력 사용시간. month가 false일경우 빈 배열.[[
          -   <월>(String) : ex) '2020-07',  '2020-08', '2020-09'
          -   usage_time(int) : 사용 시간(단위: 초)
          
          ]]
      -   day(Array): 최근 day_n일 동안의 전력 사용시간.day가 false일경우 빈 배열.[[
          -   <일>(String) : ex) '2020-09-24', '2020-09-25', '2020-09-26'
          -   usage_time(int) : 사용 시간(단위: 초)
          
          ]]
  -   error response body:

- `GET api/web/using-time/<String:year>` 

  - description : 그 해의 사용 시간을 매 월별로 보여준다. 

  - method : GET

  - URI : `/api/web/using-time<String:year>`

  - request header :

  - param: 

    - raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
    - raspberry_id(String) : 라즈베리파이 식별 아이디, 빈 문자열일 경우 그룹 내 전체 라즈베리파이를 대상으로 조회

  - request body: X

  - response header: 

  - response body: 

    - 200:

      - using_time : [{

        - "2020-01" :  사용 시간(int)

        }

      ]

  - error response body:

  - 404 (Not Found)

  

- `GET api/web/ranking`

  - description : 모든 라즈베리파이의 이번 달 순위 10위 반환

  - method : GET

  - URI : `/api/web/ranking`

  - request header :

  - param: X

  - request body: X

  - response header:

  - response body:

    - 200:

      - "ranking" : [{

        - raspberry_id:
        - raspberry_group:
        - time : 

        }

      ]

  - error response body:

