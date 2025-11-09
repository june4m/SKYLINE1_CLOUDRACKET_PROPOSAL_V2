---
title: "Ước tính ngân sách"
date: "2025-11-09"
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

# Ước tính ngân sách

Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)  
Hoặc tải [tệp ước tính ngân sách](../attachments/budget_estimation.pdf).

## Chi phí hạ tầng

### Dịch vụ AWS:
- **AWS Amplify Hosting**: Free Tier: 500 phút build, 5 GB phục vụ. Sau Free Tier: ~$0.01/phút × 500 = $5.00/tháng
- **AWS Lambda**: $0.00/tháng (20,000 requests/ngày, 128 MB, trung bình 200 ms)
- **Amazon API Gateway**: $0.00/tháng (600,000 requests/tháng, trong Free Tier)
- **Amazon DynamoDB**: $0.00/tháng (5 GB dữ liệu, 100K đọc/ghi mỗi ngày)
- **Amazon S3 (Lưu ảnh)**: $0.12/tháng (10 GB lưu trữ, 5,000 GET/PUT requests)
- **Amazon SES (Email)**: $0.00/tháng (2,000 email/tháng trong Free Tier)
- **Amazon Personalize**: Miễn phí 2 tháng đầu (20 GB dữ liệu, 5M interactions). Sau đó: ~$8.00/tháng với batch inference (dữ liệu nhỏ + huấn luyện hàng tuần).
- **Dashboard tùy chỉnh (Amplify + Chart.js)**: $0.00/tháng (sử dụng Amplify hiện có, dữ liệu từ S3/DynamoDB)
- **Amazon Location Service**: $0.00/tháng (10,000 map requests, 1,000 location requests)
- **Amazon EventBridge (Scheduler)**: $0.00/tháng (10 quy tắc kích hoạt mỗi ngày/giờ)
- **AWS IAM + KMS + WAF**: $0.00/tháng (xác thực, mã hóa và bảo mật cơ bản)

### Tổng chi phí phân bổ:
- **Tháng 1**: $0.12/tháng (tất cả trong Free Tier)
- **Tháng 2**: $5.12/tháng (Personalize vẫn trong Free Tier, Amplify bắt đầu tính phí)
- **Sau khi hết Free Tier**: $13.12/tháng, ≈ $157.44/năm

**Tổng cộng**: $0.7/tháng trong quá trình phát triển, $8.40/12 tháng chi phí ban đầu