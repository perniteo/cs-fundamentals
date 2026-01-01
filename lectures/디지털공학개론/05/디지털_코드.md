### 1. 2진 코드
- BCD
  - 구성이 간단하나, 연산 과정이 복잡
  - 사용 불가 코드가 존재
- 3초과 코드
  - BCD 코드를 이용한 연산이 어려움을 개선
  - BCD + '0011' -> **비가중치코드**
  - 자기 보수 코드이므로 연산이 가능  
- Gray Code (그레이 코드)
  - 인접한 값이 1비트만 변화
  - 값 해석보다 변화 안정성이 목적
  - 사용처:
    - 회전 엔코더
    - 위치 센서
    - ADC 변환 단계

### 2. 알파뉴메릭코드(alphanumeric code)
- ASCII Code(American Standard Code for Information Interchange Code)
  - 정보 교환용(DATA 통신용) 미국 표준코드
  - 7비트로(3개의 Zone Bit + 4개의 Digit Bit)로 구성
  - ![img.png](img.png)
- EBCDIC Code(Extended Binary Coded Decimal Interchange Code)
  - 정보 표현의 제약점을 극복하기 위해 BCD 코드를 확장한 코드
  - 8비트로 (4개의 Zone Bit + 4개의 Digit Bit)로 구성
  - ![img_1.png](img_1.png)
  - 대형 시스템의 정보 처리용으로 사용
  
### 3. 패리티 비트와 해밍코드

- 패리티 bit 기법
  - 에러 검출에 이용 (기수 또는 우수)
- 해밍 코드
  - 에러 검출 및 수정 코드
  - ![img_2.png](img_2.png)