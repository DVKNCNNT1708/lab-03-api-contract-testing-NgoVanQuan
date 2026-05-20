# Consumer–Provider Handshake

## Thông tin chung

- Lab: FIT4110 Lab 03
- Ngày: 2026-05-13
- Provider team: team-vision (AI Vision team)
- Consumer team: team-iot (IoT Ingestion team)
- Provider service: AI Vision API
- Consumer service: IoT Ingestion API

## Contract

- Contract file: contracts/ai-vision.openapi.yaml
- Mock base URL: http://localhost:4011
- Auth method: Bearer Token (JWT)
- Endpoint được test: POST /detect

## Smoke test

### Request

```http
POST http://localhost:4011/detect
Authorization: Bearer {{authToken}}
Content-Type: application/json
```

```json
{
  "camera_id": "CAM01",
  "image_url": "https://example.com/frame.jpg"
}
```

### Expected response

```json
{
  "detection_id": "DET001",
  "camera_id": "CAM01",
  "label": "person",
  "confidence": 0.91,
  "risk_level": "medium"
}
```

## Kết quả

- [x] Consumer gọi mock thành công (status 200).
- [x] Consumer parse được field cần dùng (detection_id, label, confidence).
- [x] Consumer hiểu lỗi 4xx/5xx provider trả về (ProblemDetails schema).
- [x] Có Newman report hoặc screenshot (newman-report.xml, newman-report.html).

## Ghi chú thay đổi hợp đồng

| Nội dung | Trước | Sau | Người đồng ý |
|---------|-------|-----|-------------|
| Confidence range | 0-1 | 0-1 | team-vision, team-iot |
| Risk level enum | low,medium,high | low,medium,high | team-vision, team-iot |
| Detection fields | detection_id, label, confidence | detection_id, camera_id, label, confidence, risk_level | team-vision, team-iot |

### Lưu ý

- Consumer (IoT) gọi mock API của provider (Vision) tại port 4011.
- Mock được khởi động bằng `npm run mock:vision`.
- Test này nằm trong folder `05_Consumer_side_Smoke` và kiểm tra rằng IoT service có thể hiểu và xử lý response từ Vision service.
- Khi Vision service thật được hoàn thiện, nhóm IoT cần retest bằng cách thay đổi `aiVisionMockUrl` sang URL của Vision service thật.
|---|---|---|---|
| | | | |

## Xác nhận

- Provider representative:
- Consumer representative:
