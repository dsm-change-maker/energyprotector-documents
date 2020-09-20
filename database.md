# Database



## Device

- key : Integer, primary_key - 디바이스 키 값
- id : String(64) - 디바이스 아이디
-  ip : String(32) - 디바이스 아이피
-  type : String(64) - 디바이스 타입
-  unit_count : Integer - On/Off 가능한 장치 수
- rasp_key : Integer, foreign_key - 라즈베리파이의 키 값을 가지는 외래키

| key  | ip          | type     | unit_count | rasp_key | id        |
| ---- | ----------- | -------- | ---------- | -------- | --------- |
| 1    | "127.0.0.1" | "switch" | 3          | 1        | "dsm11_1" |
| 2    | "127.0.0.2" | "button" | 2          | 1        | "dsm11_2" |

## Raspberry

- key : Integer, primary_key - 라즈베리파이 키 값
- id : String(64) - 라즈베리파이 아이디 값
- pw : String(64) - 라즈베리파이 패스워드 값
- group : String(64) - 라즈베리파이 그룹 값
- remote_control : Boolean - 라즈베리 파이 원격 제어 허용

| key  | pw     | group                      | remote_control | id      |
| ---- | ------ | -------------------------- | -------------- | ------- |
| 1    | "1234" | "대덕소프트웨어마이스터고" | True           | "dsm11" |



## Unit

- key : Integer, primary_key - 유닛 키 값
- index : Integer - 유닛들 인덱스
- device_id : Integer, foreign_key - 디바이스 키
- on_off : Boolean - 온오프
- start : Date time -  켜진 시간 저장



| key  | index | device_id | on_off | start            |
| ---- | ----- | --------- | ------ | ---------------- |
| 1    | 0     | "dsm11_1" | True   |                  |
| 2    | 1     | "dsm11_1" | False  | 2020-09-20-21:30 |
| 3    | 2     | "dsm11_1" | False  |                  |
| 4    | 0     | "dsm11_2" | True   | 2020-09-20-16:27 |
| 5    | 1     | "dsm11_2" | False  |                  |



## UsingTime

- key : Integer, primary_key
- rasp_key : Integer, foreign_key
- time : Integer(초 단위)
- date : Datetime

| key  | rasp_key | time | date       |
| ---- | -------- | ---- | ---------- |
| 1    | 1        | 324  | 2020-09-20 |



