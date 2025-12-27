네트워크1 핵심 포인트 정리
1️⃣ 네트워크 구조 / 구분

LAN: 한 건물/사무실 내부 네트워크, 속도 빠름

WAN: 지리적으로 떨어진 LAN 연결, 구현 방식 다양 (전용선, VPN, SD-WAN)

Intranet: 내부 전용망, 접근 제한 목적, LAN/WAN 위에서 구현 가능

Internet: 전 세계 네트워크 연결, 공용망

2️⃣ 주소 체계

IP 주소, 서브넷, 게이트웨이

IPv4 / IPv6 기본 구조

사설 IP vs 공인 IP → NAT 이해

3️⃣ 프로토콜 / 계층

TCP/IP 계층 구조 이해

Application (HTTP, FTP) → Transport (TCP, UDP) → Network (IP) → Data Link / Physical

캡슐화 / 역캡슐화 개념

ACK/NAK, 연결형 vs 비연결형 전송

4️⃣ 기본 네트워크 실습

ping → 연결 확인 / 지연 측정

traceroute → 경로 확인

ipconfig / ifconfig → IP 확인, 기본 정보

nslookup → DNS 조회

5️⃣ 네트워크 흐름

요청 → 캡슐화 → 전송 → 역캡슐화 → 응답

LAN/WAN/Internet을 거쳐 패킷이 이동하는 원리 이해

6️⃣ 추가 이해 포인트

VPN = 외부에서 내부망 접근 시 안전한 터널

방화벽 / ACL = 접근 제어

SDN/SD-WAN = 현대 네트워크 제어/최적화 개념