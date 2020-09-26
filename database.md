# Database



## Device

- key : Integer, primary_key - 디바이스 키

- id : String(64) - 디바이스 아이디

- type : String(64) - 디바이스 타입

- unit_count : Integer - On/Off 가능한 장치 

- ip : String(32) - 디바이스 아이피

  

| key  | id        | type     | unit_count | ip          |
| ---- | --------- | -------- | ---------- | ----------- |
| 1    | "dsm11_1" | "switch" | 3          | "127.0.0.1" |
| 2    | "dsm11_2" | "button" | 2          | "127.0.0.2" |

## Raspberry

- key : Integer, primary_key - 라즈베리파이 키 값
- id : String(64) - 라즈베리파이 아이디 값
- pw : String(64) - 라즈베리파이 패스워드 값
- group : String(64) - 라즈베리파이 그룹 값
- remote_control : Boolean - 라즈베리 파이 원격 제어 허용
- devices : Text - 라즈베리파이에 연결된 디바이스들의 id와 type 정보
- start_date : String(32) - 라즈베리를 설치하여 작동을 시작한 날짜

| key  | id      | pw     | group | remote_control | devices                          | start_date |
| ---- | ------- | ------ | ----- | -------------- | -------------------------------- | ---------- |
| 1    | "dsm11" | "1234" | "dsm" | True           | "dsm11_1;switch,dsm11_2;button," | 2020_09_26 |



## Unit

- key : Integer, primary_key - 유닛 키 값
- index : Integer - 유닛들 인덱스
- device_key : Integer, foreign_key - 디바이스 키
- on_off : Boolean - 온오프
- start : Date time -  켜진 시간 저장



| key  | index | device_key | on_off | start            |
| ---- | ----- | ---------- | ------ | ---------------- |
| 1    | 0     | 1          | True   |                  |
| 2    | 1     | 1          | False  | 2020-09-20-21:30 |
| 3    | 2     | 1          | False  |                  |
| 4    | 0     | 2          | True   | 2020-09-20-16:27 |
| 5    | 1     | 2          | False  |                  |



## UsingTime

### UsingTimeDay

- key : Integer, primary_key ; 라즈베리파이의 키 값과 같다
- time : Integer(초 단위)
- date : String(문자열)

| key  | time | date       |
| ---- | ---- | ---------- |
| 1    | 324  | 2020-09-20 |

### UsingTimeMonth

- key : Integer, primary_key - 라즈베리파이의 키 값과 같다
- time : Integer(초 단위)
- date : String(문자열)

| key  | time | date    |
| ---- | ---- | ------- |
| 1    | 324  | 2020-09 |

### UsingTimeYear

- key : Integer, primary_key - 라즈베리파이의 키 값과 같다
- time : Integer(초 단위)
- date : String(문자열)

| key  | time | date |
| ---- | ---- | ---- |
| 1    | 324  | 2020 |





