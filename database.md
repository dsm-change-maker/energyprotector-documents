# Database



## Device

- id : String(64), primary_key - 디바이스 아이디
-  ip : String(32) - 디바이스 아이피
-  type : String(64) - 디바이스 타입
-  unit_count : Integer - On/Off 가능한 장치 수
- rasp_key : Integer, foreign_key - 라즈베리파이의 키 값을 가지는 외래키



## Raspberry

- key : Integer, primary_key - 라즈베리파이 키 값
- id : String(64) - 라즈베리파이 아이디 값
- pw : String(64) - 라즈베리파이 패스워드 값
- group : String(64) - 라즈베리파이 그룹 값
- remote_control : Boolean - 라즈베리 파이 원격 제어 허용

| id    | pw   | group                    | remote_control | key  |
| ----- | ---- | ------------------------ | -------------- | ---- |
| dsm11 | 1234 | 대덕소프트웨어마이스터고 | True           | 1    |



## Unit

- index : Integer - 유닛들 인덱스
- device_id : Integer, foreign_key - 디바이스 키
- on_off : Boolean - 온오프
- start : Date time -  켜진 시간 저장



## UsingTime

- key : Integer, primary_key
- rasp_key : Integer, foreign_key
- time : Integer(초 단위)
- date : Datetime

