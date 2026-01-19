# Async / Await & Spring MVC 비동기 개념 정리

> 이 문서는 async/await, Spring MVC, Dispatcher, CPU, Thread, 비동기의 본질을  
> “왜 이렇게 동작하는가” 관점에서 정리한 노트이다.

---

## 1. Spring MVC에서 요청 흐름의 실제 책임 분리

### 구조
Client  
↓  
Tomcat (Servlet Container)

- Thread Pool 관리

- Thread 할당 / 반납  

    ↓  
DispatcherServlet (Spring MVC)

  - 요청 흐름 조율

  - Controller 매핑

  - 응답 조립

    ↓  
    Controller / Service / Repo


### 핵심
- **스레드 관리는 Spring이 하지 않는다**
- **Tomcat이 스레드 풀을 관리**
- DispatcherServlet은 **요청 흐름 관리자**일 뿐

> DispatcherServlet ≠ Thread Scheduler  
> DispatcherServlet = 요청 흐름의 PM

---

## 2. CPU의 정확한 역할 (중요)

### 흔한 오해
- CPU = 계산만 하는 존재
- 비동기 = CPU가 다른 계산을 병렬로 수행

### 실제 역할
- 실행 흐름 선택
- 상태 전환
- 이벤트 처리
- 분기 판단

> CPU는 계산기라기보다 **초고속 관리자**

### 핵심 문장
> **CPU를 거치지 않는 것은 없다.  
> 다만 CPU가 직접 일하느냐, 지시만 하느냐의 차이다.**

---

## 3. 비동기에서 “컨텍스트”란 무엇인가

### 요청 1개당 서버 메모리에 유지되는 것
- 실행 위치
- 로컬 변수
- 다음 재개 지점
- response 대상 정보

### I/O 대기 중 자원 사용
| 자원 | 사용 여부 |
|---|---|
| 메모리 | ✅ |
| 스레드 | ❌ |
| CPU | ❌ |

> 비동기는 **스레드를 반납하고 상태만 유지하는 모델**

---

## 4. 왜 I/O-bound 작업에 비동기가 유리한가

### Blocking 모델
- I/O 대기 중 스레드 점유
- CPU는 놀고 있음
- 동시 요청 수 제한

### Non-blocking 모델
- I/O 요청 등록 후 즉시 다른 흐름 처리
- CPU는 **다른 요청의 흐름을 처리**
- 스레드는 공유

> 비동기는 병렬이 아니라 **동시성(concurrency)**

---

## 5. async / await의 정체

### async
- 이 함수는 **중단·재개 가능한 함수**
- await 가능한 **비동기 인터페이스(계약)**

### await
- 실행 흐름을 **중단(suspend)**
- 컨텍스트 저장
- 스레드는 반환
- 결과(resolve) 시 **같은 컨텍스트로 재개(resume)**

### 핵심 정의
> **async/await는  
> “resolve → resume”을 자동으로 연결해주는 문법**

---

## 6. “함수가 살아 있다”는 감각

### async 함수에서 await 시
- 스레드: ❌ 기다리지 않음
- 함수: ❌ 종료되지 않음
- 실행 상태: ✅ 유지됨

기술적으로:
- 콜스택은 사라짐
- 상태 머신은 힙에 저장됨

> **기다리는 건 스레드가 아니라, 살아 있는 함수다**

---

## 7. await가 없는 async의 의미

### 오해
- await 없으면 병렬 처리

### 실제 의미
- 비동기 작업을 **시작만 해두고**
- 이 흐름에서는 **결과를 기다리지 않음**

### 정당한 사용 경우
- 인터페이스 통일
- fire-and-forget (로그, 메트릭 등)
- 프레임워크 시그니처 요구
- 테스트 / Mock

⚠️ 대부분의 경우:
> await 없는 async = **버그 가능성 큼**

---

## 8. await를 쓰려면 async가 필요한가?

### 정확한 답
- await는 **awaitable 대상**에만 사용 가능
- async는 awaitable을 만드는 **가장 일반적인 방법**

> **async = await 가능한 계약  
> await = 그 계약을 실행하는 지점**

---

## 9. Spring MVC / WebFlux / FastAPI 맥락 정리

| 구분 | MVC | WebFlux | FastAPI |
|---|---|---|---|
| 모델 | Blocking | Non-blocking | Non-blocking |
| 스레드 | 요청당 1개 | 이벤트 루프 | 이벤트 루프 |
| Dispatcher | DispatcherServlet | DispatcherHandler | 없음 (ASGI) |
| 핵심 | 규칙/도메인 | 전면 비동기 | I/O 파이프라인 |

---

## 10. 최종 핵심 문장 모음

- 비동기는 CPU를 빠르게 만드는 기술이 아니다
- CPU는 관리자다
- Dispatcher는 요청 관리자다
- await는 기다리는 게 아니라 “자리를 맡겨두는 것”
- 스레드는 기다리지 않지만, 함수는 살아 있다
- async는 약속이고, await는 중단 지점이다
- 병렬 ≠ 비동기

---