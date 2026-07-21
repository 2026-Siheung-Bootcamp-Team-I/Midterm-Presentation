# 4. 기술 설명 3-2 — React 대시보드 실시간 시연

## 구조
- **ClickHouse → Spring Boot → React** 순서로 데이터 전달
- ClickHouse의 데이터를 Spring Boot(API 서버)가 **React가 요청하는 자료 규격(API)** 으로 반환
- React는 Spring Boot에서 받은 API를 토대로 화면 출력

## 대시보드 화면
- 이벤트 추이 그래프 (시간대별 탐지 건수)
- 탐지 이벤트 목록 및 상세 정보
- 저장된 원본 로그 조회·검색

## 실시간 시연 포인트
- ClickHouse의 빠른 집계 덕분에 대용량 로그도 **실시간에 가깝게 시각화**
- 이상 행동 발생 → Slack 알림 수신 → 대시보드에서 상세 확인까지 **전체 흐름 시연**

## 예상 질문 대비
- **Kafka/Kafka Streams를 쓴 이유?** → 실시간성(0.1초 내 알림), 서버 부하 감소, 구축 간편성
- **ClickHouse가 꼭 필요한가?** → 대량 로그의 빠른 저장·집계, Streams가 버린 기록의 보관 창고
- **Slack 메시지는 어떻게 보내나?** → Incoming Webhook + JSON 페이로드 + WebClient POST
