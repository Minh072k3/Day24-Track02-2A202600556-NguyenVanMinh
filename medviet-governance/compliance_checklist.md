# NĐ13/2023 Compliance Checklist — MedViet AI Platform

## A. Data Localization
- [ ] Tất cả patient data lưu trên servers đặt tại Việt Nam
- [ ] Backup cũng phải ở trong lãnh thổ VN
- [ ] Log việc transfer data ra ngoài nếu có

## B. Explicit Consent
- [ ] Thu thập consent trước khi dùng data cho AI training
- [ ] Có mechanism để user rút consent (Right to Erasure)
- [ ] Lưu consent record với timestamp

## C. Breach Notification (72h)
- [ ] Có incident response plan
- [ ] Alert tự động khi phát hiện breach
- [ ] Quy trình báo cáo đến cơ quan có thẩm quyền trong 72h

## D. DPO Appointment
- [ ] DPO có thể liên hệ tại: dpo@medviet.vn

## E. Technical Controls (mapping từ requirements)
| NĐ13 Requirement | Technical Control | Status | Owner |
|-----------------|-------------------|--------|-------|
| Data minimization | PII anonymization pipeline (Presidio) | ✅ Done | AI Team |
| Access control | RBAC (Casbin) + ABAC (OPA) | ✅ Done | Platform Team |
| Encryption | AES-256 at rest, TLS 1.3 in transit | ✅ Done | Infra Team |
| Audit logging | CloudTrail + API access logs | ⬜ Todo | Platform Team |
| Breach detection | Anomaly monitoring (Prometheus) | ⬜ Todo | Security Team |

## F. Giải pháp kỹ thuật cho phần Todo
- **Audit logging**: Sử dụng Elasticsearch, Logstash, Kibana (ELK stack) hoặc CloudTrail để lưu trữ và phân tích logs truy cập API và database. Đảm bảo logs không thể bị xóa hoặc sửa đổi (immutable logs).
- **Breach detection**: Tích hợp Prometheus và Grafana để theo dõi các bất thường về lưu lượng truy cập mạng. Sử dụng AWS GuardDuty hoặc các công cụ IDS/IPS để phát hiện xâm nhập và cảnh báo kịp thời qua Slack/Email.
