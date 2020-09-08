# APIs

에너지 지킴이 프로젝트의 API 명세 및 Description

## APIs 목차

-   [공통](#공통)
-   [Device API](#device-api)
-   [RaspberryPi API](#raspberrypi-api)
-   [Usage-Time API](#usage-time-api)

## 공통

-   모든 API request, response의 `Content-Type`은 `application/json`이다.
-   모든 API의 response body에는 성공 여부(or 정상 동작 여부) - is_success(Boolean)을 포함한다.

## Device API

-   `GET /api/device` - 디바이스 등록 정보 조회 API
    -   description : 등록된 디바이스에 대한 정보를 가져옵니다.
    -   method : GET
    -   URI : /api/device
    -   request header :X
    -   param:
        -   device_id(String) : 가져올 디바이스의 식별 아이디
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 조회 성공 여부
        -   device_id(String) : 디바이스의 식별 아이디
        -   device_type(String) : 디바이스의 유형
        -   motor_count(Integer) : ON/OFF 가능한 서보모터의 개수
        -   connected_raspberry(String) : 연결된 라즈베리파이의 식별 아이디. 연결되지 않았으면 빈 문자열
-   `POST /api/device` - 디바이스 등록 API
    -   description : 새로운 디바이스에 대한 정보를 등록합니다.
    -   method : POST
    -   URI : /api/device
    -   request header :
        -   `Content-Type` : `application/json`
    -   param : X
    -   request body:
        -   device_id(String) : 디바이스 식별 아이디
        -   device_type(String) : 디바이스의 유형(스위치 or 플러그 or ETC …)
        -   motor_count(int) : ON/OFF 가능한 서보모터의 개수
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 등록 성공 여부
-   `PUT /api/device` - 디바이스 등록 정보 수정 API
    -   description : 등록된 디바이스 정보를 수정합니다.
    -   method : PUT
    -   URI : /api/device
    -   request header :
        -   `Content-Type` : `application/json`
    -   param: X
    -   request body:
        -   device_id(String) : 수정할 디바이스의 식별 아이디
        -   device_type(String) : 디바이스의 유형을 이 값으로 수정
        -   motor_count(int) : ON/OFF 가능한 서보모터의 개수를 이 값으로 수정
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 등록 수정 성공 여부
-   `DELETE /api/device` - 디바이스 등록 정보 삭제 API
    -   description : 등록된 디바이스 정보를 삭제합니다.
    -   method : DELETE
    -   URI : /api/device
    -   request header : X
    -   param:
        -   device_id(String) : 삭제할 디바이스의 식별 아이디
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 삭제 성공 여부.

## RaspberryPi API

-   `GET /api/raspberry` - 라즈베리파이 등록 정보 조회 API
    -   description : 라즈베리파이 등록 정보를 가져옵니다.
    -   method : GET
    -   URI : /api/raspberry
    -   request header : X
    -   param :
        -   raspberry_id(String) : 조회할 라즈베리파이 식별 아이디
    -   request body: X
    -   response header :
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 조회 성공 여부
        -   raspberry_id(String) : 조회한 라즈베리파이 식별 아이디
        -   raspberry_devices(Array) :
            -   device_id : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
            -   device_type : 조회한 라즈베리파이에 연결된 디바이스 유형
-   `POST /api/raspberry` - 라즈베리파이 등록 API
    -   description : 새로운 라즈베리파이 정보를 등록합니다.
    -   method: POST - URI : /api/raspberry
    -   request header :
        -   `Content-Type` : `application/json`
    -   param: X
    -   request body
        -   raspberry_id(String) : 라즈베리파이 식별 아이디(디바이스 연결 시 사용)
        -   raspberry_pw(String) : 라즈베리파이 비밀번호(디바이스 연결 시 사용)
        -   raspberry_devices(Array) :
            -   device_id : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
            -   device_type(String) : 조회한 라즈베리파이에 연결된 디바이스 유형
    -   response header:
        -   `Content-Type`: `application/json`
    -   response body:
        -   is_success(Boolean): 등록 성공 여부
-   `PUT /api/raspberry` - 라즈베리파이 등록 정보 수정 API
    -   description : 등록된 라즈베리파이 정보를 수정합니다.
    -   method: POST - URI : /api/raspberry
    -   request header :
        -   `Content-Type` : `application/json`
    -   param: X
    -   request body
        -   raspberry_id(String) : 라즈베리파이 식별 아이디(디바이스 연결 시 사용)
        -   raspberry_pw(String) : 수정할 라즈베리파이 비밀번호(디바이스 연결 시 사용)
        -   raspberry_devices(Array) :
            -   device_id(String) : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
            -   device_type(String) : 조회한 라즈베리파이에 연결된 디바이스 유형
    -   response header:
        -   `Content-Type`: `application/json`
    -   response body:
        -   is_success(Boolean): 수정 성공 여부
-   `DELETE /api/raspberry` - 라즈베리파이 등록 정보 삭제 API
    -   description : 등록된 라즈베리파이 정보를 삭제합니다.
    -   method : DELETE
    -   URI : /api/raspberry
    -   request header : X
    -   param:
        -   raspberry_id(String) : 삭제할 라즈베리파이의 식별 아이디
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 삭제 성공 여부.

## Usage-Time API

-   `GET /api/usage-time` - 사용시간 조회 API
    -   description : 라즈베리파이의 전력 사용시간을 조회합니다.
    -   method: GET
    -   URI: /api/usage-time
    -   request header: X
    -   param:
        -   raspberry_id(String) : 라즈베리파이 식별 아이디
        -   year(Boolean) : 최근 year_n년동안의 전력 사용시간 조회. False 시 조회하지 않음
        -   year_n(Integer) : 최근 몇 년을 조회할 것인지 결정. year가 False일 경우 의미 없음. 유효하지 않은 값일 경우 기본 값 1.
        -   month(Boolean) : 최근 month_n달동안의 전력 사용시간 조회. False 시 조회하지 않음.
        -   month_n(Integer) : 최근 몇 달을 조회할 것인지 결정. month가 False일 경우 의미없음. 유효하지 않은 값일 경우 기본 값 1.
        -   week(Boolean) : 최근 week_n주동안의 전력 사용시간 조회. False 시 조회하지 않음
        -   week_n(Integer) : 최근 몇 주를 조회할 것인지 결정. week가 False일 경우 의미없음. 유효하지 않은 값일 경우 기본 값 1.
        -   day(Boolean) : 최근 day_n일 동안의 전력 사용시간 조회. False 시 조회하지 않음.
        -   day_n(Integer) : 최근 며칠을 조회할 것인지 결정. day가 False일 경우 의미없음. 유효하지 않은 값일 경우 기본 값 1.
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean): 조회 성공 여부
        -   usage_times:
            -   year(Array): 최근 year_n년 동안의 전력 사용시간. year가 false일경우 빈 배열.
            -   month(Array): 최근 month_n달 동안의 전력 사용시간. month가 false일경우 빈 배열.
            -   week(Array): 최근 week_n주 동안의 전력 사용시간.week가 false일경우 빈 배열.
            -   day(Array): 최근 day_n일 동안의 전력 사용시간.day가 false일경우 빈 배열.
