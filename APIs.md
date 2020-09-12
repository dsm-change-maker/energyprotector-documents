# APIs

에너지 지킴이 프로젝트의 API 명세 및 Description

## APIs 목차

-   [공통](#공통)
-   [API Response 구조](#api-response-구조)
-   [Device API](#device-api)
-   [Device Control API](#device-control-api)
-   [RaspberryPi API](#raspberrypi-api)
-   [Usage-Time API](#usage-time-api)

## 공통

-   모든 API request, response의 `Content-Type`은 `application/json`이다.
-   모든 API의 response body에는 성공 여부 - is_success(Boolean)을 포함한다.

## API Response 구조

-   code(Integer) : 응답 코드
-   message(String) : 에러메시지
-   data : 해당 API의 response body

예시)

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

## Device API

-   `GET /api/device` - 디바이스 등록 정보 조회 API
    -   description : 등록된 디바이스에 대한 정보를 가져옵니다.
    -   method : GET
    -   URI : /api/device
    -   request header :X
    -   param:
        -   device_id(String) : 디바이스의 식별 아이디
        -   raspberry_group(String) : 제어하고자 하는 디바이스가 현재 연결된 라즈베리파이의 그룹 아이디. 어느 곳에도 연결되지 않은 디바이스 조회시 빈 문자열.
        -   raspberry_id(String) : 제어하고자 하는 디바이스가 현재 연결된 라즈베리파이의 식별 아이디. 어느 곳에도 연결되지 않은 디바이스 조회시 빈 문자열.
        -   raspberry_pw(String) : 제어하고자 하는 디바이스가 현재 연결된 라즈베리파이의 비밀번호. 어느 곳에도 연결되지 않은 디바이스 조회시 빈 문자열.
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 조회 성공 여부
        -   device_id(String) : 디바이스의 식별 아이디
        -   device_type(String) : 디바이스의 유형
        -   device_ip(String) : 디바이스 IP Address
        -   unit_count(Integer) : ON/OFF 가능한 장치의 개수
        -   on_off(Array) :
            -   (Boolean) : 디바이스에 연결된 ON/OFF 가능한 장치들의 ON/OFF 상태
    -   response body 예시:

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true,
        "device_id": "UDLC_7d1df214",
        "device_type": "Plug",
        "device_ip": "127.0.0.1",
        "unit_count": 3,
        "on_off": [true, false, false]
    }
}
```

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
        -   device_ip(String) : 디바이스 IP Address
        -   unit_count(Integer) : ON/OFF 가능한 장치의 개수(스위치라고 하면 서보모터의 개수, 플러그이면 SSR의 개수)
        -   on_off(Array) :
            -   (Boolean) : 디바이스에 연결된 ON/OFF 가능한 장치들의 ON/OFF 초기 상태
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 등록 성공 여부

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

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
        -   device_ip(String) : 디바이스 IP Address
        -   unit_count(int) : ON/OFF 가능한 장치의 개수를 이 값으로 수정
        -   on_off(Array) :
            -   (Boolean) : 디바이스에 연결된 ON/OFF 가능한 장치들의 ON/OFF 상태.
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 등록 수정 성공 여부

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

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

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

## Device Control API

-   `POST /api/device/control` - 디바이스 제어 API
    -   description : 디바이스의 상태(ON/OFF)를 변화시킵니다.
    -   method : POST
    -   URI: /api/device/control
    -   request header:
        -   `Content-Type`:`application/json`
    -   param: X
    -   request body:
        -   device_id(String): 제어할 디바이스의 식별 아이디
        -   on_off(Boolean): true일경우 ON, false일경우 OFF
        -   raspberry_group(String):디바이스에 연결된 라즈베리파이 그룹 아이디
        -   raspberry_id(String): 디바이스에 연결된 라즈베리파이 아이디
        -   raspberry_pw(String):디바이스에 연결된 라즈베리파이 비밀번호
    -   response header:
        -   `Content-Type`:`application/json`
    -   response body:
        -   is_success(Boolean) : 성공 여부

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

## RaspberryPi API

-   `POST /api/raspberry/connect` - 라즈베리파이 등록 정보 조회 API
    -   description : 라즈베리파이 등록 정보를 가져옵니다.
    -   method : POST
    -   URI : /api/raspberry/connect
    -   request header :
        -   `Content-Type`:`application/json`
    -   param : X
    -   request body:
        -   raspberry_group(String) : 조회할 그룹
        -   raspberry_id(String) : 조회할 라즈베리파이 식별 아이디
        -   raspberry_pw(String) : 조회할 라즈베리파이 비밀번호
    -   response header :
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 조회 성공 여부
        -   raspberry_group(String) : 조회할 그룹
        -   raspberry_id(String) : 라즈베리파이 식별 아이디
        -   remote_control(Boolean) : 원격 제어 허용/비허용. 비허용 시 웹/앱 등에서 라즈베리파이에 연결 불가능. 만약 False 시 raspberry_devices는 빈 배열.
        -   raspberry_devices(Array) :
            -   device_id : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
            -   device_type(String) : 조회한 라즈베리파이에 연결된 디바이스 유형

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true,
        "raspberry_group": "DSM_OMHU_4de773090",
        "raspberry_id": "FKW7_4de7730d7",
        "remote_control": true,
        "raspberry_devices": [
            {
                "device_id": "PL4J_4de773130",
                "device_type": "Switch"
            },
            {
                "device_id": "LUTK_4de773145",
                "device_type": "Plug"
            }
        ]
    }
}
```

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
        -   raspberry_devices(Array) :
            -   device_id : 조회한 라즈베리파이에 연결된 디바이스 식별 아이디
            -   device_type(String) : 조회한 라즈베리파이에 연결된 디바이스 유형
    -   response header:
        -   `Content-Type`: `application/json`
    -   response body:
        -   is_success(Boolean): 등록 성공 여부

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

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
    -   response header:
        -   `Content-Type`: `application/json`
    -   response body:
        -   is_success(Boolean): 수정 성공 여부

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

-   `DELETE /api/raspberry` - 라즈베리파이 등록 정보 삭제 API
    -   description : 등록된 라즈베리파이 정보를 삭제합니다.
    -   method : DELETE
    -   URI : /api/raspberry
    -   request header : X
    -   param:
        -   raspberry_group(String) : 삭제할 라즈베리파이가 속한 그룹 아이디
        -   raspberry_id(String) : 삭제할 라즈베리파이의 식별 아이디
    -   request body: X
    -   response header:
        -   `Content-Type` : `application/json`
    -   response body:
        -   is_success(Boolean) : 삭제 성공 여부.

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```

## Usage-Time API

-   `GET /api/usage-time` - 사용시간 조회 API
    -   description : 라즈베리파이의 전력 사용시간을 조회합니다.
    -   method: GET
    -   URI: /api/usage-time
    -   request header: X
    -   param:
        -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
        -   raspberry_id(String) : 라즈베리파이 식별 아이디, 빈 문자열일 경우 그룹 내 전체 라즈베리파이를 대상으로 조회
        -   sort(Boolean) : usage_time을 기준으로 true시 오름차순 정렬. false시 내림차순 정렬.
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

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true,
        "usage_times": {
            "year": [
                {
                    "raspberry_id": "8NVS_7ca58504",
                    "usage_time": 257.47 // 257시간 47분
                }
            ],
            "month": [],
            "week": [],
            "day": []
        }
    }
}
```

-   `POST /api/usage-time` - 사용시간 저장 API
    -   description : 특정 라즈베리파이의 하루 전력 사용시간을 저장합니다.
    -   method: POST
    -   URI: /api/usage-time
    -   request header:
        -   `Content-Type`:`application/json`
    -   param: X
    -   request body:
        -   raspberry_group(String) : 라즈베리파이가 속한 그룹 아이디
        -   raspberry_id(String) : 라즈베리파이 식별 아이디
        -   raspberry_pw(String) : 라즈베리파이의 비밀번호
        -   usage_time(Integer) : 사용 시간
        -   date(String) : 측정 날짜
    -   response header:
        -   `Content-Type`:`application/json`
    -   response body:
        -   is_success(Boolean):성공 여부

```json
{
    "code": 200,
    "message": "",
    "data": {
        "isSuccess": true
    }
}
```
