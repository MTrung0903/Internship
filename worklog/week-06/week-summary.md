# Tóm tắt tuần (19/05/2025 - 25/05/2025)

## 📅 Tổng quan
- **Tuần**: Tuần 6/12 của chương trình thực tập
- **Thời gian**: 19/05/2025 - 25/05/2025
- **Tâm trạng**: 😊 Duy trì thái độ tích cực, hào hứng với các bài lab về Amazon FSx, S3, và CloudFront
- **Tiến độ tổng thể**: Hoàn thành 100% Module 02, 100% Module 03, và 100% Module 04

## 🎯 Thành tựu chính
- **Hoàn thành Module 04 (Lab)**:
  - **Lab 04-25**: Kiểm tra hiệu suất FSx với DiskSpd/fio, giám sát qua CloudWatch, kích hoạt data deduplication, shadow copies, quản lý user sessions/open files, thiết lập user storage quotas, tạo Continuous Access Share cho SQL Server, mở rộng throughput/storage capacity, và dọn dẹp môi trường.
  - **Lab 04-57**: Tạo S3 bucket, tải source code, bật static website hosting, cấu hình public access block và public objects, kiểm tra website, chặn public access, cấu hình CloudFront, kiểm tra CloudFront, kích hoạt bucket versioning, di chuyển objects, thiết lập Cross-Region Replication (CRR), và dọn dẹp tài nguyên.
- **Phát triển kỹ năng**:
  - **Kỹ năng kỹ thuật**: Thành thạo Amazon FSx (performance, deduplication, shadow copies, quotas, Continuous Access Share, scaling), S3 (static website, public access, versioning, CRR), CloudFront (CDN), và quản lý tài nguyên.
  - **Kỹ năng mềm**: Cải thiện ghi chú chi tiết, quản lý thời gian, tự học qua AWS Documentation và video AWS Study Group, xử lý lỗi cấu hình.
  - **Kiến thức ngành**: Hiểu vai trò của FSx trong môi trường Windows, S3 và CloudFront trong hosting website tĩnh, CRR trong disaster recovery, và các giải pháp tối ưu hóa hiệu suất/chi phí.

## 💼 Công việc đã thực hiện
- **Ngày 19/05**: Hoàn thành Module 04-Lab25-04, 05, 06 (Kiểm tra hiệu suất FSx, giám sát qua CloudWatch, kích hoạt data deduplication, dọn dẹp tài nguyên).
- **Ngày 20/05**: Hoàn thành Module 04-Lab25-07, 08, 09 (Kích hoạt shadow copies, quản lý user sessions/open files, thiết lập user storage quotas).
- **Ngày 21/05**: Hoàn thành Module 04-Lab25-10, 11, 12, 13 (Tạo Continuous Access Share cho SQL Server, mở rộng throughput/storage capacity, dọn dẹp môi trường).
- **Ngày 22/05**: Hoàn thành Module 04-Lab57-02.1, 02.2, 03 (Tạo S3 bucket, tải source code, bật static website hosting).
- **Ngày 23/05**: Hoàn thành Module 04-Lab57-04, 05, 06 (Cấu hình public access block, public objects, kiểm tra website tĩnh).
- **Ngày 24/05**: Hoàn thành Module 03-Lab57-07.1, 07.2, 07.3, 08, 09 (Chặn public access, cấu hình CloudFront, kiểm tra CloudFront, kích hoạt versioning, di chuyển objects).
- **Ngày 25/05**: Hoàn thành Module 04-Lab57-09, 10, 11 (Di chuyển objects, thiết lập S3 CRR, dọn dẹp tài nguyên).

## 📚 Kiến thức học được
- **Kỹ thuật**:
  - **Dịch vụ AWS**: Amazon FSx, S3, CloudFront, CloudWatch, SNS, Secrets Manager, IAM, CloudFormation.
  - **Công cụ**: AWS Management Console, AWS CLI, DiskSpd, fio, Windows PowerShell, File Explorer, Remote Desktop, Web Browser (Chrome), Developer Tools, Notion (ghi chú).
  - **Kiến trúc**: Tích hợp FSx với Windows Active Directory, S3 với CloudFront cho website tĩnh, CRR cho disaster recovery, và tối ưu hóa hiệu suất với FSx scaling.
- **Lý thuyết**:
  - **Amazon FSx**: Hỗ trợ shadow copies, user quotas, Continuous Access Share, và scaling throughput/storage.
  - **S3**: Static website hosting, public access block, ACLs, versioning, Cross-Region Replication (CRR).
  - **CloudFront**: CDN để giảm latency và tăng bảo mật cho website tĩnh.
  - **CloudWatch**: Giám sát hiệu suất FSx và thiết lập alarm.
  - **Data Deduplication**: Giảm dung lượng lưu trữ bằng cách loại bỏ dữ liệu trùng lặp.
  - **Performance Testing**: Sử dụng DiskSpd/fio để đo I/O, Developer Tools để đo thời gian tải trang.
- **Kỹ năng mềm**:
  - Ghi chú chi tiết, quản lý thời gian, tự học qua AWS Documentation và video AWS Study Group.
  - Giải quyết vấn đề: Xử lý lỗi cấu hình FSx (failover, deduplication), S3 (public access, CRR), CloudFront (cache), và bucket versioning.
  - Trực quan hóa kiến trúc qua sơ đồ draw.io.

## 🚧 Khó khăn và giải pháp


## 💭 Phản ánh và nhận xét
- **Thành công**:
  - Hoàn thành 100% Module 04, bao gồm các bài lab về FSx (performance, deduplication, shadow copies, quotas, Continuous Access Share, scaling) và S3/CloudFront (static website, versioning, CRR).
  - Thành thạo cấu hình FSx, S3, CloudFront, và quản lý tài nguyên.
  - Dọn dẹp tài nguyên sau mỗi lab, tránh phát sinh chi phí.
- **Cần cải thiện**:
  - Tăng cường kiểm tra cấu hình (failover, versioning, ACLs) trước khi thực hành để giảm lỗi.
  - Ghi lại thời gian chi tiết cho từng nhiệm vụ để quản lý hiệu quả.
  - Tăng tương tác với mentor và cộng đồng AWS để học hỏi thêm.
- **Nhận xét**:
  - FSx là giải pháp mạnh mẽ cho các ứng dụng Windows cần lưu trữ chia sẻ và HA (như SQL Server).
  - S3 và CloudFront cung cấp giải pháp hosting website tĩnh hiệu quả, với CRR đảm bảo disaster recovery.
  - CloudWatch và data deduplication giúp tối ưu hóa hiệu suất và chi phí cho FSx.

## 📋 Kế hoạch tuần tới
- **Ưu tiên**:
  - Hoàn thành Lab 03-02 (EC2 Auto Scaling với EFS).
  - Tìm hiểu và thực hành tích hợp Auto Scaling với Elastic Load Balancing.
  - Đọc tài liệu và thực hành AWS Application Migration Service (MGN).
- **Mục tiêu học tập**:
  - Hiểu cách cấu hình Auto Scaling Group và tích hợp EFS.
  - Nắm quy trình triển khai ứng dụng với Elastic Load Balancing.
  - Tìm hiểu quy trình di chuyển ứng dụng với AWS MGN.

## 📊 Đánh giá bản thân
- **Năng suất**: 9/10 (Hoàn thành nhiều nhiệm vụ, nhưng cần cải thiện kiểm tra cấu hình và ghi thời gian chi tiết).
- **Học tập**: 9/10 (Nắm được kiến thức về FSx, S3, CloudFront, CRR, và các công cụ như DiskSpd/fio).
- **Hợp tác**: 5/10 (Chưa có tương tác với mentor hoặc team, cần cải thiện).
- **Hài lòng tổng thể**: 9/10 (Tiến độ tốt, nhưng cần thực hành nhiều hơn với CloudFront invalidation và tương tác với cộng đồng).

## 📎 Tài liệu và liên kết
- **Tài liệu học tập**:
  - [AWS Study Group Videos](https://www.youtube.com/@AWSStudyGroup)
  - [AWS FSx for Windows File Server Documentation](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is-fsx-windows.html)
  - [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
  - [AWS CloudFront Documentation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
  - [AWS CloudWatch Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
  - [Module 04-Lab25](https://000025.awsstudygroup.com/)
  - [Module 04-Lab57](https://000057.awsstudygroup.com/)
- **Ghi chú và dự án**:
  - [Notes](https://docs.google.com/document/d/1K7j883rmdA2oahmKZ26OYYqE9cLMg1a4lCY64stBprk/edit?usp=sharing)
  - [Sơ đồ FSx Architecture](https://drive.google.com/file/d/1zTQjhTUXg4rnyFKJEjZdoQfFejCTUm_s/view?usp=sharing)

---

**📝 Ghi chú cho tuần tới**:
- Chuẩn bị môi trường AWS để thực hành Lab 03-02 (EC2 Auto Scaling với EFS).
- Đọc trước tài liệu về Elastic Load Balancing và AWS MGN.
- Lên lịch trao đổi với mentor để thảo luận về Module 04 và kế hoạch tuần tới.

**🎯 Tiến độ tuần**: Hoàn thành 100% Module 02, 100% Module 03, 100% Module 04 (Module 04-01, 04-02, 04-03, 04-04, Lab 04-13, Lab 04-14, Lab 04-24, Lab 04-25, Lab 04-57).

---
*Week summary created by: Hồ Minh Trung*  
*Next review: 26/05/2025*