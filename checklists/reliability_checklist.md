# Reliability Checklist — FIT4110 Lab 03

Điền checklist này trước khi nộp Lab 03.

## 1. Functional tests

- [x] Có test cho endpoint health.
- [x] Có test happy path cho endpoint chính (/readings POST).
- [x] Có kiểm tra status code 2xx (201 Created).
- [x] Có kiểm tra field quan trọng trong response (reading_id, device_id, metric, accepted).
- [x] Có ít nhất 1 test đọc dữ liệu danh sách hoặc chi tiết (/readings/latest).

## 2. Auth tests

- [x] Có test thiếu token (TC05 - skipped on mock, checked on local).
- [x] Có test sai token hoặc token rỗng (TC06 - invalid token test).
- [x] Endpoint public được khai báo rõ nếu không cần auth (/health không cần auth).
- [x] Test thể hiện đúng expected status 401/403 (requests without token expect 401).

## 3. Negative tests

- [x] Có test thiếu field bắt buộc (TC07 - missing device_id).
- [x] Có test sai kiểu dữ liệu (TC08 - invalid metric enum value).
- [x] Có test sai enum hoặc giá trị ngoài miền (metric=temp_hot, value=81).
- [x] Lỗi trả về theo cùng một error model (ProblemDetails với type, title, status, detail).

## 4. Boundary tests

- [x] Có test min/max hoặc dữ liệu sát ngưỡng (TC09 - temperature=80 at max boundary).
- [x] Có test limit/pagination nếu endpoint có danh sách (TC11 - limit parameter boundary).
- [x] Có test payload lớn hoặc metadata thiếu (boundary value 81 out of range).
- [x] Có ghi chú kỳ vọng xử lý dữ liệu biên (temperature range -40 to 80 documented in contract).

## 5. Reliability tests cơ bản

- [x] Có kiểm tra response time (TC13 - local only latency check).
- [x] Có mô tả timeout mong muốn (1000ms threshold for local service).
- [x] Có test hoặc ghi chú retry/idempotency nếu phù hợp (idempotency implicit via reading_id).
- [x] Có consumer-side smoke test với ít nhất 1 mock của nhóm khác (TC12 - calls AI Vision /detect).

## 6. Evidence

- [x] Collection export JSON (FIT4110_lab03_iot_ingestion.postman_collection.json).
- [x] Environment mock export JSON (FIT4110_lab03_mock.postman_environment.json).
- [x] Environment local export JSON (FIT4110_lab03_local.postman_environment.json).
- [x] Newman report XML/HTML (generated via npm run test:mock, test:html).
- [x] Test-case matrix đã điền (test-case-matrix.csv with 13 test cases).
- [x] Biên bản handshake đã điền (consumer-provider-handshake.md).
