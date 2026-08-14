# TCP 3-Way Handshake 실습

## 목적

Wireshark를 이용하여 TCP 연결 과정에서 발생하는 3-Way Handshake 패킷을 캡처하고 분석한다.

SYN, SYN + ACK, ACK 패킷의 역할을 확인하여 TCP 연결이 수립되는 과정을 이해한다.

## 환경

- OS: Windows
- Tool: Wireshark 4.6.8
- Protocol: TCP

---

# 1. TCP 패킷 캡처

Wireshark를 실행한 후 현재 사용 중인 네트워크 인터페이스인 Ethernet을 선택하여 패킷 캡처를 시작한다.

TCP 패킷을 확인하기 위해 표시 필터에 다음 명령어를 입력한다.

```bash
tcp

이후 웹사이트에 접속하여 새로운 TCP 연결을 발생시키고 관련 패킷을 확인한다.

2. TCP 3-Way Handshake 분석

TCP 연결 과정에서 다음과 같은 순서로 패킷이 교환되는 것을 확인하였다.

① SYN
클라이언트 → 서버


② SYN + ACK
서버 → 클라이언트


③ ACK
클라이언트 → 서버

실제 패킷에서는 다음과 같은 통신을 확인하였다.

192.168.219.100:50550
        ↓ SYN
172.66.147.243:443
        ↓ SYN + ACK
192.168.219.100:50550
        ↓ ACK
TCP 연결 수립
실행 결과

<img width="1203" height="444" alt="3-way Handshake 1" src="https://github.com/user-attachments/assets/a894a343-7857-4122-b342-d0be640077cb" />


그림 1. Wireshark를 이용한 TCP 3-Way Handshake 패킷 분석

패킷 분석

SYN

클라이언트인 192.168.219.100에서 서버 172.66.147.243의 443번 포트로 TCP 연결을 요청하는 SYN 패킷을 확인하였다.

SYN + ACK

서버가 클라이언트의 SYN 패킷을 수신한 후 SYN과 ACK를 함께 전송하여 연결 요청에 응답하는 것을 확인하였다.

ACK

클라이언트가 서버의 SYN + ACK를 확인한 후 ACK 패킷을 전송하는 것을 확인하였다.

이 과정이 완료되면서 TCP 연결이 수립된다.

3. 보안 관점

TCP 3-Way Handshake는 네트워크 통신의 기본적인 연결 수립 과정으로 네트워크 트래픽 분석과 보안관제 업무에서도 중요한 개념이다.

비정상적으로 많은 SYN 패킷이 특정 서버로 반복적으로 발생하거나 연결이 정상적으로 완료되지 않는 경우 SYN Flood와 같은 네트워크 공격을 의심할 수 있다.

따라서 보안관제에서는 TCP 연결 패턴과 패킷 흐름을 분석하여 비정상적인 네트워크 활동을 탐지할 수 있다.

4. 실습 결과

Wireshark를 이용하여 실제 TCP 패킷을 캡처하고 SYN, SYN + ACK, ACK 패킷을 분석하였다.

이를 통해 TCP 연결이 SYN → SYN + ACK → ACK 순서의 3-Way Handshake 과정을 통해 수립되는 것을 실제 패킷을 기반으로 확인하였다.

면접 포인트

Wireshark를 활용하여 TCP 패킷을 직접 캡처하고 SYN, SYN/ACK, ACK 패킷을 분석하여 TCP 연결 수립 과정을 확인할 수 있다.
