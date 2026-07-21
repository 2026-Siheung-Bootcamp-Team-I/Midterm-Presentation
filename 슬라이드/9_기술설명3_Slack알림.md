# 4. 기술 설명 3-1 — Spring Boot · Slack 알림 연동

## 동작 원리 3단계

### ① Incoming Webhook — 외부 노출용 단방향 통로
- 원래 외부 서버가 Slack 채널에 메시지를 쓰려면 복잡한 인증(OAuth)이 필요
- Incoming Webhook은 이를 단순화 — Slack 채널과 1:1로 매핑된 **고유 URL** 발급
- 이 URL은 일종의 **'비밀 우체통' 주소** — 규격에 맞는 데이터를 넣으면 Slack이 채널에 자동 표시

### ② JSON 데이터 페이로드 — 데이터 규격화
- Slack은 지정된 **JSON 형식**만 인식
- 가장 단순한 형태: `{"text": "보낼 내용"}`
- 버튼, 굵은 글씨, 색상 띠 등 꾸미기는 **Block Kit** JSON 구조 사용

### ③ HTTP 클라이언트 발송 — Spring Boot
- 이벤트 발생 시(위협 탐지 등) 내장 HTTP 클라이언트로 요청 발송
- 최신 Spring 환경에서는 비동기/논블로킹 지원 **WebClient** 사용
- Webhook URL을 목적지로 JSON을 HTTP Body에 실어 **POST 요청**

## 전체 흐름

```
[이벤트 발생] → [Spring Boot에서 JSON 조립] → [WebClient로 Webhook URL에 POST] → [Slack 채널에 알림 표시]
```
