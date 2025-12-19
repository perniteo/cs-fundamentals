# 네트워크1 핵심 노트

## 1. 네트워크 구조 / 구분
- **LAN (Local Area Network)**  
  - 범위: 사무실/건물 내부  
  - 특징: 속도 빠름, 지연 낮음
- **WAN (Wide Area Network)**  
  - 범위: 지리적으로 떨어진 LAN 연결  
  - 구현 방식: 전용선, 인터넷 + VPN, MPLS, SD-WAN
- **Intranet (내부 전용망)**  
  - 목적: 접근 제한, 내부 서비스 제공  
  - LAN/WAN 위에서 구현 가능
- **Internet**  
  - 전 세계 연결, 공용망

## 2. 주소 체계
- IP 주소, 서브넷, 게이트웨이  
- IPv4 / IPv6 구조  
- 사설 IP vs 공인 IP (NAT 이해)

## 3. 프로토콜 / 계층
- **TCP/IP 계층 구조**  
  - Application (HTTP, FTP)  
  - Transport (TCP, UDP)  
  - Network (IP)  
  - Data Link / Physical
- 캡슐화 / 역캡슐화  
- ACK/NAK, 연결형 vs 비연결형 전송

## 4. 기본 실습 명령어
- `ping` → 연결 확인 / 지연 측정  
- `traceroute` → 경로 확인  
- `ipconfig` / `ifconfig` → IP 확인, 네트워크 정보  
- `nslookup` → DNS 조회

## 5. 네트워크 흐름
1. 요청(Request) 생성  
2. 캡슐화 후 전송  
3. 패킷이 LAN/WAN/Internet 경로 이동  
4. 목적지에서 역캡슐화  
5. 응답(Response) 반환

## 6. 추가 포인트
- VPN → 외부에서 내부망 접근 안전하게  
- 방화벽 / ACL → 접근 제어  
- SDN / SD-WAN → 현대 네트워크 제어/최적화