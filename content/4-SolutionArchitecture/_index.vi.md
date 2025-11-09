---
title: "Kiến trúc giải pháp"
date: "2025-11-09"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---



Nền tảng áp dụng kiến trúc AWS Serverless giúp vận hành ổn định, dễ mở rộng và tiết kiệm chi phí. Dữ liệu về người dùng, sân và lịch đặt được lưu trữ trong Amazon DynamoDB. Giao tiếp giữa các thành phần thông qua Amazon API Gateway và các hàm AWS Lambda. Giao diện web và di động được triển khai bằng AWS Amplify, trong khi Amazon Cognito đảm bảo kiểm soát truy cập an toàn.

Amazon Personalize gợi ý sân dựa trên lịch sử người dùng và Amazon Comprehend cân nhắc sân dựa trên bình luận và sao đánh giá, Custom Dashboard sẽ trực quan hóa dữ liệu hoạt động cho chủ sân và người dùng. Tất cả hoạt động được giám sát qua Amazon CloudWatch và tự động hóa bằng Amazon EventBridge.


![Cloud Racket Platform Architecture](/images/2-Proposal/Skyline1_CloudRacket.jpg)

## Dịch vụ AWS sử dụng
- **AWS Amplify Hosting**: Lưu trữ và triển khai ứng dụng web/mobile.
- **Amazon API Gateway**: Giao tiếp giữa client và backend.
- **AWS Lambda**: Xử lý logic nghiệp vụ và kết nối các dịch vụ AWS.
- **Amazon DynamoDB**: Lưu trữ thông tin người dùng, sân và lịch đặt.
- **Amazon Cognito**: Xác thực và phân quyền người dùng.
- **Amazon SES**: Gửi email xác nhận và thông báo tự động.
- **Amazon S3**: Lưu trữ hình ảnh sân và dữ liệu phân tích.
- **Amazon Personalize**: Đưa ra gợi ý sân phù hợp cho người dùng.
- **Amazon Comprehend (Optional)**: phân tích cảm xúc trong bình luận tiếng Việt để bổ sung điểm đánh giá tổng hợp.
- **Amazon Location Service + DynamoDB GeoLib**: Tìm kiếm sân gần vị trí người dùng.
- **Custom Dashboard**: Trực quan hóa dữ liệu và phân tích báo cáo thông qua bảng điều khiển tùy chỉnh (Custom Dashboard) được xây dựng bằng AWS Amplify, AWS Lambda, và biểu đồ Chart.js từ dữ liệu lưu trong Amazon DynamoDB hoặc Amazon S3.
- **Amplify Admin UI (Admin Portal)**: quản lý CRUD sân, duyệt bình luận, theo dõi logs.
- **Amplify CI/CD**: Tự động triển khai và cập nhật hệ thống.
- **Amazon CloudWatch**: Theo dõi log, hiệu suất và cảnh báo.
- **Amazon EventBridge (Scheduler)**: Tự động hóa lịch gửi thông báo và dọn dẹp dữ liệu.
- **AWS IAM + KMS + WAF**: Quản lý bảo mật, mã hóa dữ liệu và ngăn chặn tấn công web.

## Thiết kế thành phần
- **User Module**: Amazon Cognito quản lý đăng ký, đăng nhập và hồ sơ người dùng; dữ liệu người chơi, lịch sử đặt sân và sân yêu thích lưu trong DynamoDB.
- **Court Module**: Chủ sân thêm, chỉnh sửa thông tin và ảnh sân; dữ liệu sân lưu trong DynamoDB, hình ảnh trên S3; cập nhật trạng thái sân qua API Gateway + Lambda.
- **Booking Flow**: API Gateway → Lambda → DynamoDB → SES xử lý đặt sân, kiểm tra trùng lịch và gửi email xác nhận tự động.
- **Recommendation System**: Amazon Personalize phân tích hành vi và đánh giá người dùng để gợi ý sân; Lambda truy vấn kết quả gợi ý theo mô hình 70% hành vi + 30% rating.
- **Geo Search**: DynamoDB Geo Library hoặc Amazon Location Service tìm sân gần vị trí người chơi; tích hợp Google Maps hiển thị bản đồ và hướng đi.
- **Admin Dashboard**: Bảng điều khiển tùy chỉnh hiển thị doanh thu, lượt đặt và đánh giá, được xây dựng bằng AWS Amplify và Chart.js, với dữ liệu tổng hợp từ DynamoDB hoặc S3 thông qua AWS Lambda.
- **Automation Layer**: EventBridge kích hoạt Lambda định kỳ để gửi nhắc lịch, huấn luyện lại Personalize và dọn dữ liệu cũ.